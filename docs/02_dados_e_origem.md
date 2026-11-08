# 2. Dados e origem

## Origem

Todos os dados são **sintéticos (fictícios)**. A base foi gerada para fins de demonstração e entregue em um pacote inicial (datado de 21/10/2026). Nenhum registro vem de uma empresa, cliente ou pessoa real: os nomes de clientes e vendedores são inventados.

## Arquivos (pasta `data/`)

| Arquivo | Conteúdo | Linhas |
|---|---|---|
| `FatoVendas.csv` | Itens de pedidos e valores | 8.611 |
| `DimCalendario.csv` | Calendário diário 2024–2025 | 731 |
| `DimClientes.csv` | Clientes e localização | 180 |
| `DimProdutos.csv` | Catálogo de produtos | 18 |
| `DimVendedores.csv` | Equipe de vendas | 8 |
| `Base_Dashboard_Vendas.xlsx` | As cinco tabelas em um único Excel | — |

## Resumo da base

- Período: 01/01/2024 a 31/12/2025.
- 5.200 pedidos distintos, em 8.611 linhas (um pedido pode ter vários itens).
- 180 clientes, 18 produtos, 8 vendedores.
- Status do pedido: **Faturado** (4.358 pedidos), **Devolvido** (385) e **Cancelado** (457). Nesta base, cada pedido tem um único status.
- Sem valores nulos na tabela fato.

## Preparação no Power Query

- Conferência dos tipos de dados (datas como Data, quantidades como inteiro, valores como decimal).
- Conferência dos valores de `Status` e das chaves antes de criar os relacionamentos.
- Nenhuma limpeza pesada foi necessária, porque a base já vem estruturada.

## Observação sobre o uso

Qualquer conclusão extraída deste dashboard vale somente para esta base fictícia.
