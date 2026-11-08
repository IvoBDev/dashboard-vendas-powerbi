# 4. Modelo e medidas DAX

## Modelo (esquema em estrela)

```
DimCalendario ─┐
DimClientes ───┤
DimProdutos ───┼──► FatoVendas
DimVendedores ─┘
```

Uma tabela fato (`FatoVendas`) e quatro dimensões, com relacionamentos 1:* em uma direção. `DimCalendario` está marcada como tabela de datas, e `Mes` é ordenada por `MesNumero`. Todas as medidas ficam na tabela `_Medidas`.

## Regras de negócio

| Conceito | Definição |
|---|---|
| Receita Faturada | Soma de `ValorVenda` dos itens com status Faturado |
| Valor Devolvido | Valor dos itens Devolvidos, exibido como número positivo |
| **Receita Líquida** | Receita Faturada − Valor Devolvido |
| Custo Líquido | Custo dos itens Faturados − custo dos itens Devolvidos |
| Margem Bruta % | (Receita Líquida − Custo Líquido) ÷ Receita Líquida |
| Taxa de Devolução | Pedidos devolvidos ÷ (faturados + devolvidos) |
| Taxa de Cancelamento | Pedidos cancelados ÷ (faturados + devolvidos + cancelados) |

## Medidas

Receita e margem:

```DAX
Receita Faturada =
CALCULATE ( SUM ( FatoVendas[ValorVenda] ); FatoVendas[Status] = "Faturado" )

Valor Devolvido =
-CALCULATE ( SUM ( FatoVendas[ValorVenda] ); FatoVendas[Status] = "Devolvido" )

Receita Líquida =
[Receita Faturada] - [Valor Devolvido]

Custo Líquido =
CALCULATE ( SUM ( FatoVendas[CustoTotal] ); FatoVendas[Status] = "Faturado" )
    - CALCULATE ( SUM ( FatoVendas[CustoTotal] ); FatoVendas[Status] = "Devolvido" )

Lucro Bruto Estimado =
[Receita Líquida] - [Custo Líquido]

Margem Bruta % =
DIVIDE ( [Lucro Bruto Estimado]; [Receita Líquida] )

Descontos Concedidos =
CALCULATE ( SUM ( FatoVendas[ValorDesconto] ); FatoVendas[Status] = "Faturado" )
```

Pedidos e vendas:

```DAX
Pedidos =
CALCULATE ( DISTINCTCOUNT ( FatoVendas[PedidoID] ); FatoVendas[Status] = "Faturado" )

Quantidade Vendida =
CALCULATE ( SUM ( FatoVendas[Quantidade] ); FatoVendas[Status] = "Faturado" )

Ticket Médio =
DIVIDE ( [Receita Faturada]; [Pedidos] )
```

Devoluções e cancelamentos:

```DAX
Pedidos Devolvidos =
CALCULATE ( DISTINCTCOUNT ( FatoVendas[PedidoID] ); FatoVendas[Status] = "Devolvido" )

Taxa de Devolução =
DIVIDE ( [Pedidos Devolvidos]; [Pedidos] + [Pedidos Devolvidos] )

Pedidos Cancelados =
CALCULATE ( DISTINCTCOUNT ( FatoVendas[PedidoID] ); FatoVendas[Status] = "Cancelado" )

Taxa de Cancelamento =
DIVIDE ( [Pedidos Cancelados]; [Pedidos] + [Pedidos Devolvidos] + [Pedidos Cancelados] )
```

Clientes:

```DAX
Clientes Ativos =
CALCULATE ( DISTINCTCOUNT ( FatoVendas[ClienteID] ); FatoVendas[Status] = "Faturado" )

Receita por Cliente =
DIVIDE ( [Receita Líquida]; [Clientes Ativos] )

Pedidos por Cliente =
DIVIDE ( [Pedidos]; [Clientes Ativos] )
```

Comparação com o ano anterior (criadas e testadas, mas não aparecem nas páginas finais):

```DAX
Receita Líquida Ano Anterior =
IF (
    HASONEVALUE ( DimCalendario[Ano] );
    CALCULATE ( [Receita Líquida]; SAMEPERIODLASTYEAR ( DimCalendario[Data] ) )
)

Variação YoY % =
DIVIDE ( [Receita Líquida] - [Receita Líquida Ano Anterior]; [Receita Líquida Ano Anterior] )
```

A condição `HASONEVALUE` é necessária: sem ela, com 2024 e 2025 no mesmo contexto, a comparação mostrava uma variação de cerca de +104%, que não faz sentido.

Medidas de interface (selo de filtros ativos):

```DAX
Qtd Filtros Ativos =
VAR n =
    IF ( ISFILTERED ( DimCalendario[Ano] ); 1; 0 )
        + IF ( ISFILTERED ( DimClientes[Regiao] ); 1; 0 )
        + IF ( ISFILTERED ( DimProdutos[Categoria] ); 1; 0 )
        + IF ( ISFILTERED ( FatoVendas[Canal] ); 1; 0 )
RETURN
    IF ( n > 0; n )

Cor Selo =
IF ( [Qtd Filtros Ativos] >= 1; "#299D91"; "#191919" )

Cor Texto Selo =
IF ( [Qtd Filtros Ativos] >= 1; "#FFFFFF"; "#191919" )
```

Observação: os separadores acima são ponto e vírgula, como no Power BI em português. Em instalações em inglês, troque por vírgula. Use o nome da coluna exatamente como aparece no seu modelo (por exemplo `Regiao`, com ou sem acento).

## Por que as medidas são em camadas

O pacote inicial trazia uma medida de margem que **penalizava a devolução duas vezes**: abatia a receita devolvida, mas mantinha o custo da mercadoria devolvida. Por isso as medidas foram refeitas em camadas (Receita Líquida → Custo Líquido → Lucro → Margem), com a premissa descrita em [Premissas e limitações](05_premissas_e_limitacoes.md).
