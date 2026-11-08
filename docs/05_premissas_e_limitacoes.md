# 5. Premissas e limitações

## Premissas

1. **Base fictícia.** Nenhum número representa uma empresa real, e nenhuma conclusão de negócio deve ser tirada daqui.
2. **Receita Líquida** = receita faturada menos o valor devolvido. Pedidos cancelados não geram receita.
3. **Custo das devoluções.** As mercadorias devolvidas são consideradas **de volta ao estoque**, então o custo delas é abatido do Custo Líquido. Em uma empresa real, parte da devolução poderia virar perda (defeito, avaria), e a margem seria menor.
4. **Margem Bruta % é uma estimativa simulada.** O custo vem da própria base fictícia e não considera frete, impostos, comissões nem despesas.
5. **Pedidos** contam apenas pedidos faturados (contagem distinta de `PedidoID`). Nesta base, cada pedido tem um único status, e a soma de faturados, devolvidos e cancelados fecha em 5.200 pedidos.
6. **Ticket Médio** usa a Receita Faturada (antes das devoluções) dividida pelos pedidos faturados.

## Limitações conhecidas

- **Unidades de exibição:** os gráficos mostram valores em "Mil" ou "Mi". O arredondamento pode gerar diferenças pequenas entre a soma dos rótulos e o total do cartão.
- **Gráfico de produtos:** sem rótulos de valor (ficaram apertados). O valor aparece na dica de ferramenta ao passar o mouse. Alguns nomes de produto aparecem truncados no eixo.
- **Comparação anual (YoY):** foi testada e retirada do layout. As medidas existem no modelo, mas nenhuma página as usa.
- **Navegação do Desktop:** os botões e bookmarks funcionam com Ctrl + clique no Power BI Desktop. A experiência é pensada para o Desktop; o arquivo não foi publicado no Power BI Service.
- **Versão do Power BI:** o arquivo foi criado numa versão recente do Desktop. Versões antigas podem não exibir alguns visuais ou formatações.
- **Sem atualização automática:** os dados vêm de arquivos estáticos.
- **Acessibilidade:** o texto alternativo dos visuais ainda não foi preenchido. É uma melhoria prevista.
- **Modelo:** a tabela `DimProdutos` traz a coluna `MargemBase`, que não é usada nas medidas.
