# 6. Validação dos números

Cada medida foi conferida contra um cálculo independente feito diretamente sobre os CSVs (fora do Power BI). Valores sem filtro:

| Medida | Valor de referência | No dashboard |
|---|---|---|
| Receita Faturada | R$ 6.129.612,02 | confere |
| Valor Devolvido | R$ 465.101,38 | confere |
| **Receita Líquida** | **R$ 5.664.510,64** | R$ 5.664.511 |
| Custo Líquido | R$ 4.598.305,86 | confere |
| Lucro Bruto Estimado | R$ 1.066.204,78 | R$ 1.066.205 |
| Margem Bruta % | 18,8% | 18,8% |
| Pedidos | 4.358 | 4.358 |
| Quantidade Vendida | 14.254 | confere |
| Ticket Médio | R$ 1.406,52 | R$ 1.407 |
| Descontos Concedidos | R$ 439.084,25 | R$ 439.084 |
| Pedidos Devolvidos | 385 | confere |
| Taxa de Devolução | 8,1% | 8,1% |
| Clientes Ativos | 180 | 180 |
| Receita por Cliente | R$ 31.469,50 | R$ 31.470 |
| Pedidos por Cliente | 24,2 | 24,2 |
| Pedidos Cancelados | 457 | confere |
| Taxa de Cancelamento | 8,8% | 8,8% |
| Receita Líquida 2024 | R$ 2.769.444,61 | confere |
| Receita Líquida 2025 | R$ 2.895.066,03 | confere |

## Por categoria, região, canal e segmento (sem filtro)

| Dimensão | Valores (receita líquida, em milhões) |
|---|---|
| Categoria | Eletrônicos 3,33 · Escritório 1,32 · Rede 0,56 · Acessórios 0,45 |
| Região | Sudeste 1,59 · Nordeste 1,29 · Sul 1,22 · Centro-Oeste 0,80 · Norte 0,77 |
| Canal | E-commerce 2,04 · Vendas internas 1,32 · Loja física 1,24 · Representante 1,07 |
| Segmento | Pessoa Física 2,77 · Pequena 1,49 · Média 0,81 · Grande 0,59 |

Margem bruta estimada por categoria: Acessórios 25,6% · Rede 20,5% · Escritório 19,2% · Eletrônicos 17,5%.

Valor devolvido por categoria: Eletrônicos R$ 270.260 · Escritório R$ 99.301 · Rede R$ 56.458 · Acessórios R$ 39.083.

## Validação cruzada

As somas por região, categoria e vendedor fecham no mesmo total da Receita Líquida (aprox. R$ 5.664 mil), dentro do arredondamento dos rótulos.

## Testes com filtros combinados

| Filtros | Receita Líquida esperada | Resultado |
|---|---|---|
| Ano = 2025 e Região = Sudeste | R$ 828.091,55 | confere |
| Categoria = Eletrônicos e Canal = E-commerce | R$ 1.213.348,69 | confere |
| Ano = 2024, Região = Norte e Categoria = Rede | R$ 39.185,88 | confere |

## Desempenho

O Performance Analyzer do Power BI Desktop mostrou o visual mais lento em cerca de **0,58 s**, na primeira rodada.
