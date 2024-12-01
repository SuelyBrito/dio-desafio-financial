# dio-desafio-financial

**Estruturação do Modelo**
 
**1. Tabela Principal (Backup):**

•	Tabela Financials (modo oculto – backup): 
	A tabela "Financials" servirá como backup e  base para criar as tabelas de dimensão e a tabela fato. Ela será mantida oculta no modelo de dados.
 
**2. Criação das Tabelas Dimensão:**

**2.1 Dim_Produtos:**

•	Esta tabela  contém informações gerais sobre os produtos, como o ID_produto e métricas referentes à  vendas.

•	**Colunas a serem criadas :** 

•         ID_produto: Chave primária do produto.

•         Produto: Nome ou descrição do produto.

•         Média de Unidades Vendidas: Média de unidades vendidas.

•         Média do valor de vendas: Média do preço de vendas.

•         Mediana do valor de vendas: Mediana do preço de vendas.

•         Valor máximo de Venda: Maior preço de venda registrado.

•         Valor mínimo de Venda: Menor preço de venda registrado.


**DAX para criar  as medidas:**

•	  Média de Unidades Vendidas: Média_Unidades_Vendidas = AVERAGE(Financials[Units Sold])

•	  Média do valor de vendas: Média_Venda = AVERAGE(Financials[Sales Price])

•	  Mediana do valor de vendas: Mediana_Venda = MEDIANX(Financials, Financials[Sales Price])

•	  Valor máximo de Venda: Max_Venda = MAX(Financials[Sales Price])

•	  Valor mínimo de Venda: Min_Venda = MIN(Financials[Sales Price])

•	  Índice de Produtos: Podemos criar um índice de produtos usando uma fórmula DAX com base em uma condição específica, como, por exemplo, Rank dos produtos mais vendidos.

•	  Índice_Produto = RANKX(ALL(D_Produtos), [Média de Unidades Vendidas], , DESC)


**2.2 Dim_Produtos_Detalhes:**

•       Esta tabela contém  detalhes adicionais sobre o produto, incluindo preço, descontos e unidades vendidas.

•	**Colunas a serem criadas:** 

•         ID_Produtos: Chave substituta (gerada automaticamente pelo Power BI).

•         Discount Band: Faixa de desconto.

•         Units Sold: Unidades vendidas.

•         Sale Price: Preço de venda do produto.

**2.3 Dim_Descontos:**

•	Esta tabela contém  os descontos aplicados aos produtos.

•	**Colunas a serem criadas:** 

•         ID_Produtos: Chave substituta (gerada automaticamente pelo Power BI).

•         Discount: Valor do desconto.

•         Discount Band: Faixa de desconto.


**2.4 Dim_Detalhes:**

•	Tabela para informações complementares, relacionadas aos produtos ou as transações efetivadas, conforme necessário.

•	Poderemos incluir nesta tabela colunas  não relacionadas  nas tabelas anteriores. Por exemplos: Produto, Segmento, País, Vendedor, Lucro, etc.

•	**Colunas a serem criadas:** 

•         ID_Produtos: Chave substituta (gerada automaticamente pelo Power BI).

•         Id_Produto : Código do Produto.
	
•         Segment : Segmento do Produto.
	
•         Country : Pais das vendas.
 
•         Sales   : Vendas.
	
•         Profit  : Lucro das Vendas.
	
•         Month Number : Numero referente ao mês das Vendas.
	
•         Month Name   : Nome do mês referente às Vendas.
	
•         Year  : Ano referente às Vendas.  

**2.5 Dim_Calendário:**

•	Tabela  criada por meio da função DAX usando CALENDAR(), que gera um intervalo de datas.

•	Exemplo: D_Calendário = CALENDAR(DATE(2013, 1, 1), DATE(2014, 12, 31)).

•       Essa função  cria uma tabela de datas de 1º de janeiro de 2013 até 31 de dezembro de 2014, que pode ser usada para análise temporal (mês, trimestre, ano, etc.).
	
•       As datas escolhidas são as contempladas na Tabela Finacial.

**3. Tabela Fato:**

•      Esta Tabela  registra as  movimentações de vendas, utilizando dados das tabelas de dimensão.

•      Fato_Vendas:
       
•    **Colunas a serem criadas:**

•       SK_Produtos: Chave substituta (gerada automaticamente pelo Power BI).

•       ID_Produto: Chave estrangeira referenciando a tabela Dim_Produtos.
	
•       Segment: Segmento de mercado.

•       Country: País de venda.

•       Produto: Nome do produto.

•       Discount Band: Faixa de desconto.

•       Units Sold: Quantidade de unidades vendidas.

•       Manufacturing Price : Preço de fabricação.

•       Sales Price: Preço de venda.

•       Sales : Vendas.

•       Profit: Lucro gerado pela transação.
•       Date: Data da venda.

**4. Relações entre as tabelas:**

•      Estabeleça as relações entre as tabelas: 

•      Dim_Produtos → Fato_Vendas: Relacionamento entre ID_Produto.

•      Dim_Descontos → Fato_Vendas: Relacionamento entre ID_Produtos.

•      Dim_Produtos_Detalhes → Fato_Vendas: Relacionamento entre Id_Produtos.

•      Dim_Calendar → Fato_Vendas: Relacionamento entre Date (Data).

**5. Salvar e Submeter:**

•      Após a criação de todas as tabelas, medidas e relacionamentos, o arquivo .pbix deve ser salvo.

•      Também crie uma imagem do seu diagrama em estrela para documentar o modelo de dados.

•      No README do repositório no GitHub, escreva sobre o processo de construção, as funcionalidades DAX usadas e uma explicação geral de como o modelo foi estruturado.

**6. Etapas e Funções DAX Utilizadas:**

•      Funções de agregação como AVERAGE(), MAX(), MIN(), MEDIANX().

•      Função de calendário: CALENDAR() para a criação da tabela de datas.

•      Função de relacionamento entre tabelas, permitindo uma visão unificada dos dados.


**7. Modelo de Dados**

https://github.com/SuelyBrito/dio-desafio-financial/blob/main/modelo.png

**8. Resultado Final:**

•      A finalidade do modelo Star Schema é oferecer possibilidades de   executar consultas de vendas, calcular o lucro total, comparar segmentos de mercado, entre outras análises. 

•      Isso permitirá acesso a  uma base sólida para construir o modelo de dados proposto  no Power BI com foco em um esquema estrela para análise de vendas e produtos.
