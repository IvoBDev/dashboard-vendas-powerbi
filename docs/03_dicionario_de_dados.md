# 3. Dicionário de dados

## FatoVendas (uma linha por item de pedido)

| Coluna | Tipo | Descrição |
|---|---|---|
| PedidoID | Texto | Identificador do pedido (ex.: PV000001). Um pedido pode ter vários itens |
| DataPedido | Data | Data do pedido. Liga com `DimCalendario[Data]` |
| ClienteID | Texto | Chave do cliente. Liga com `DimClientes` |
| ProdutoID | Texto | Chave do produto. Liga com `DimProdutos` |
| VendedorID | Texto | Chave do vendedor. Liga com `DimVendedores` |
| Canal | Texto | E-commerce, Loja física, Vendas internas ou Representante |
| Status | Texto | Faturado, Devolvido ou Cancelado |
| Quantidade | Inteiro | Unidades do item |
| PrecoUnitario | Decimal | Preço unitário de venda |
| DescontoPct | Decimal | Percentual de desconto aplicado (0,15 = 15%) |
| ValorBruto | Decimal | Quantidade × preço unitário, antes do desconto |
| ValorDesconto | Decimal | Valor do desconto em reais |
| ValorVenda | Decimal | Valor líquido do item. **Positivo** se Faturado, **negativo** se Devolvido, **zero** se Cancelado |
| CustoTotal | Decimal | Custo do item. Positivo em Faturado e Devolvido, zero em Cancelado |

## DimCalendario

| Coluna | Tipo | Descrição |
|---|---|---|
| Data | Data | Chave do calendário (tabela de datas) |
| Ano | Inteiro | 2024 ou 2025 |
| MesNumero | Inteiro | 1 a 12 (usado para ordenar `Mes`) |
| Mes | Texto | Janeiro a Dezembro |
| Trimestre | Texto | T1 a T4 |
| AnoMes | Texto | Formato AAAA-MM |
| DiaSemana | Texto | Segunda-feira a Domingo |
| FimDeSemana | Texto | Sim ou Não |

## DimClientes

| Coluna | Tipo | Descrição |
|---|---|---|
| ClienteID | Texto | Chave (ex.: CL0001) |
| Cliente | Texto | Nome fictício |
| Segmento | Texto | Pessoa Física, Pequena Empresa, Média Empresa ou Grande Empresa |
| Regiao | Texto | Norte, Nordeste, Centro-Oeste, Sudeste ou Sul |
| Estado | Texto | Nome do estado |
| UF | Texto | Sigla do estado |
| Cidade | Texto | Capital, Interior, Região Metropolitana ou Litoral (tipo de cidade, não nome real) |

## DimProdutos

| Coluna | Tipo | Descrição |
|---|---|---|
| ProdutoID | Texto | Chave (ex.: PR001) |
| Produto | Texto | Nome do produto |
| Categoria | Texto | Eletrônicos, Escritório, Rede ou Acessórios |
| PrecoLista | Decimal | Preço de tabela |
| MargemBase | Decimal | Margem de referência usada para gerar a base. **Não é usada nas medidas do dashboard** |

## DimVendedores

| Coluna | Tipo | Descrição |
|---|---|---|
| VendedorID | Texto | Chave (ex.: V001) |
| Vendedor | Texto | Nome fictício |
| RegiaoBase | Texto | Região de atuação do vendedor |

## Relacionamentos

Todos 1:* (um para muitos), filtro em uma direção, das dimensões para a fato:

- `DimCalendario[Data]` → `FatoVendas[DataPedido]`
- `DimClientes[ClienteID]` → `FatoVendas[ClienteID]`
- `DimProdutos[ProdutoID]` → `FatoVendas[ProdutoID]`
- `DimVendedores[VendedorID]` → `FatoVendas[VendedorID]`

Não há relacionamento entre as dimensões.
