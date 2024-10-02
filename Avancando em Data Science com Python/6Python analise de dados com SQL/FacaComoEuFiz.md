**Faça Como Eu Fiz** = **Mão na Massa**

## Aula 1
### Preparando o ambiente  
Neste curso, vamos aprender a integrar as linguagens SQL e Python, a partir de consultas e análises de dados.

Antes de começar…
Para fazer este curso junto comigo, você vai precisar baixar o notebook do curso.

Além disso, nosso ambiente de trabalho será o Google Colaboratory e, para que você consiga usá-lo, é necessário ter uma conta Gmail, pois todo notebook ficará armazenado no Google Drive.

Dados do curso
Iremos utilizar dados de uma empresa fictícia chamada Meteora, e os dados que vamos analisar estão disponíveis a partir de links. Se você baixou o notebook do curso e vai utilizá-lo, os links de acesso já estão disponíveis no notebook.

No entanto, caso opte por não utilizar o notebook do curso, abaixo estão os links de dados em código:

url_itens_pedidos = 'https://github.com/alura-cursos/SQL-python-integracao/raw/main/TABELAS/itens_pedidos.csv'
url_pedidos = 'https://github.com/alura-cursos/SQL-python-integracao/raw/main/TABELAS/pedidos.csv'
url_produto = 'https://github.com/alura-cursos/SQL-python-integracao/raw/main/TABELAS/produtos.csv'
url_vendedores = 'https://github.com/alura-cursos/SQL-python-integracao/raw/main/TABELAS/vendedores.csv'
Copiar código
Dicionário de dados
Abaixo uma descrição das colunas presentes em cada tabela de dados da Meteora.

Tabela vendedores
Coluna	Descrição
nome_vendedor	Nome do vendedor
vendedor_id	Identificador do vendedor
Tabela itens pedidos
Coluna	Descrição
estado	Estado para onde o pedido foi enviado
frete	Valor do frete cobrado para o envio do produto
id_nf	Identificador da nota fiscal do pedido
pedido_id	Identificador do pedido
produto_id	Identificador do produto
quantidade	Quantidade de pedidos
valor_total	Valor total dos pedidos
valor_unitario	Valor por unidade do pedido
Tabela produto
Coluna	Descrição
condicao	Condição do produto
marca	Marca do produto
preco	Preço do produto
produto	Nome do produto
produto_id	Identificador do produto
sku	Identificador do produto no estoque
Total	Número total de produtos
Tabela pedido
Coluna	Descrição
data_compra	Data de compra do pedido
pedido_id	Identificador do pedido
produto_id	Identificador do produto
total	Número total de pedidos
vendedor_id	Identificador do vendedor


## Aula 2
### Desafio: explorando mais análises  
Vamos fixar os conteúdos aprendidos através de mais análises que podem ser feitas no banco de dados. Então, os desafios propostos aqui irão sugerir encontrar e exibir informações referentes ao banco de dados.

Para os desafios, sugiro continuar com as mesmas tabelas já inseridas no banco ('itens_pedidos', 'pedidos', 'produtos', 'vendedores') e também utilizar a mesma função de execução de consulta (sql_df). Para esse curso, preparamos seis desafios que vão te ajudar a colocar a mão na massa e praticar bastante! Aqui na aula 2, deixamos os dois primeiros desafios. Na aula 3, você vai encontrar os desafios 3 e 4, na aula 4, você encontra os desafios 5 e 6.

Esse primeiro desafio vai ser constituído de duas análises, a primeira tem por objetivo calcular a receita total obtida com a venda de itens. Na tabela itens_pedidos, o valor total dos itens representa o cálculo da quantidade pelo valor unitário e pode ser considerado como a receita da venda.

Já a segunda análise visa identificar quais as 15 marcas que foram as mais pedidas por quantidades de venda. Busque mostrar essa lista em uma visualização, além de expor o nome das marcas.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.  

### Opinião do instrutor  
Podem existir diversas formas de solucionar uma questão. Irei apresentar como eu solucionei os problemas e não quer dizer que essa é a melhor solução, mas é uma opção de solução.

Desafio 1: receita total das vendas de itens
Foi feita a seleção da coluna valor_total da tabela itens_pedidos em uma query enviada na função sql_df. A receita é calculada com a soma dos valores na coluna valor_total. O valor de receita é numérico.

df_itens_pedidos = sql_df('SELECT VALOR_TOTAL FROM ITENS_PEDIDOS')
receita = df_itens_pedidos['valor_total'].sum()
receita
Copiar código
Uma outra opção é usar a função de agregação SUM() do SQL aplicada à coluna valor_total.

query = '''SELECT SUM(VALOR_TOTAL) AS RECEITA
FROM ITENS_PEDIDOS;
'''
df_itens_pedidos = sql_df(query)
df_itens_pedidos
Copiar código
Obtemos um DataFrame com o dado da receita como mostrado abaixo.

Receita
0	45803930
Desafio 2: 15 marcas mais pedidas
Foram selecionadas as marcas na tabela PRODUTOS e agrupamos elas por frequência através da função COUNT e, para obter as marcas mais vendidas, relacionamos as tabelas PRODUTOS e ITENS_PEDIDOS. O agrupamento é feito pelas marcas e ordenando os dados das tabelas.

Depois, foi feita a plotagem da visualização mostrando as 15 marcas mais vendidas na Meteora.

query = '''SELECT PRODUTOS.MARCA, COUNT (*) AS 'Pedidos'
FROM PRODUTOS, ITENS_PEDIDOS
WHERE PRODUTOS.PRODUTO_ID = ITENS_PEDIDOS.PRODUTO_ID
GROUP BY PRODUTOS.MARCA
ORDER BY COUNT(*) ASC;
'''
df_marcas = sql_df(query)

plt.barh(df_marcas['marca'][-15:], df_marcas['Pedidos'][-15:], color = '#9353FF')
plt.xlabel('Pedidos')
plt.show()  

## Aula 3
### Desafio: exibindo diferentes resultados  
Vamos aproveitar esse espaço para fixar os conteúdos aprendidos durante as aulas. Para isso, serão propostos desafios que irão sugerir encontrar e exibir informações referentes ao banco de dados.

Esse desafio vai ser constituído de dois casos para exibir informação, e neles não será necessário construir um gráfico, mas caso queira, fique a vontade para criar uma visualização ou estilizar as tabelas do desafio.

Vamos aos desafios dessa aula, o primeiro é exibir os 10 produtos mais vendidos durante o ano de 2019, que podem ser representados em uma tabela. Já o segundo será publicar a distribuição através dos meses da receita obtida em vendas no ano de 2021. Busque mostrar essa distribuição colocando o mês e sua receita correspondente na visualização.

Vale relembrar que é interessante continuar com as mesmas tabelas já inseridas no banco ('itens_pedidos', 'pedidos', 'produtos', 'vendedores') e também utilizar a mesma função de execução de consulta (sql_df) para resolver os desafios.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

  

### Opinião do Instrutor  
Podem existir diversas formas de solucionar uma questão. Irei apresentar como eu solucionei os problemas e não quer dizer que essa é a melhor solução, mas é uma opção de solução.

Desafio 3: 10 produtos mais vendidos em 2019
Inicia-se selecionando os produtos da tabela "produtos" e contando quantos pedidos existem para cada produto. Em seguida, são filtrados os resultados apenas para os pedidos feitos no ano de 2019 com strftime('%Y', data_compra) = '2019' no WHERE. Depois, os dados são agrupados por produto, ou seja, todos os pedidos relacionados a um mesmo produto são agrupados. Para que o produto mais popular apareça primeiro, os resultados são ordenados de acordo com o número total de pedidos em ordem decrescente. Por fim, a consulta retorna apenas os 10 produtos mais populares em 2019 com LIMIT.

query = '''SELECT PRODUTOS.PRODUTO, COUNT (PEDIDOS.PEDIDO_ID) AS TOTAL_PEDIDOS
FROM PEDIDOS, PRODUTOS
WHERE strftime('%Y', data_compra) = '2019' AND PEDIDOS.PRODUTO_ID = PRODUTOS.PRODUTO_ID
GROUP BY PRODUTOS.PRODUTO
ORDER BY TOTAL_PEDIDOS DESC
LIMIT 10;
'''
sql_df(query)
Copiar código
Desafio 4: distribuição da receita por mês em 2021
A consulta seleciona o mês da coluna data_compra formatado como %m usando a função strftime e o renomeia como mes. Em seguida, é calculado o total das receitas utilizando a função SUM e esse cálculo é renomeado como receita. Essa soma é feita com base na coluna total. A cláusula WHERE é utilizada para filtrar os dados apenas para o ano de 2021. A função strftime é novamente utilizada para extrair o ano (%Y) da coluna data_compra e compará-lo com o valor '2021'. Os resultados são então agrupados por mês, utilizando a cláusula GROUP BY mes.

query = '''SELECT strftime('%m', data_compra) AS mes, SUM(total) AS receita
FROM pedidos
WHERE strftime('%Y', data_compra) = '2021'
GROUP BY mes;
'''
sql_df(query)

## Aula 4
## Desafio: outras informações para a Meteora  
Nessa atividade podemos fixar os conteúdos aprendidos durante as aulas. Para isso, serão propostos desafios que irão sugerir encontrar e exibir informações referentes ao banco de dados.

Nesse desafio, vamos continuar no contexto de contribuir nas ações da Meteora de incrementar suas vendas no estado de São Paulo e, para isso, será preciso construir dois novos conjuntos de informações. Neles não será necessário construir um gráfico, mas caso queira fique a vontade para criar uma visualização ou estilizar as tabelas do desafio.

Vamos aos desafios! A intenção da Meteora é iniciar sua ação no mês de dezembro em São Paulo, aproveitando as compras de natal para divulgar os produtos e lançar promoções para pedidos feitos nesse estado. Pensando nisso, vamos fornecer duas informações que podem contribuir na ação de dezembro.

A primeira informação é listar as marcas vendidas em São Paulo por quantidade de pedidos, que podem ser representadas em uma tabela. Já a segunda informação é publicar os produtos que são mais vendidos na época de Natal no Brasil todo. Essa última informação é aplicada a todos os estados porque somente o estado de São Paulo pode não trazer uma quantidade relevante de informações.

Vale relembrar que é interessante continuar com as mesmas tabelas já inseridas no banco ('itens_pedidos', 'pedidos', 'produtos', 'vendedores') e também utilizar a mesma função de execução de consulta (sql_df) para resolver os desafios.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.  
### Opinião do Instrutor  
Podem existir diversas formas de solucionar uma questão. Irei apresentar como eu solucionei os problemas e não quer dizer que essa é a melhor solução, mas é uma opção de solução.

Desafio 5: marcas em São Paulo por quantidade de pedidos
Primeiro, é selecionada a coluna de MARCA da tabela PRODUTOS e contada a quantidade de registros. Depois, é executado um JOIN entre as tabelas PRODUTOS e ITENS_PEDIDOS, ligando-as pelo campo PRODUTO_ID. É aplicado um filtro com WHERE para considerar apenas os registros em que o estado é São Paulo ('BR-SP'). Os dados são finalmente agrupados pela coluna MARCA e ordenados em ordem decrescente com base na contagem de produtos vendidos. O resultado é uma tabela contendo uma lista ordenada das marcas com maior número de produtos vendidos.

query = '''SELECT PRODUTOS.MARCA, COUNT(*) AS 'Produtos vendidos'
FROM PRODUTOS
JOIN ITENS_PEDIDOS ON ITENS_PEDIDOS.PRODUTO_ID = PRODUTOS.PRODUTO_ID
WHERE ITENS_PEDIDOS.ESTADO = 'BR-SP'
GROUP BY PRODUTOS.MARCA
ORDER BY COUNT(ITENS_PEDIDOS.PRODUTO_ID) DESC;
'''
df_marcas_sp = sql_df(query)
df_marcas_sp
Copiar código
Desafio 6: produtos mais vendidos em dezembro no Brasil
A consulta executa a seleção da coluna de PRODUTO da tabela PRODUTOS e conta a quantidade de registros. Em seguida, é realizado um JOIN entre as tabelas PRODUTOS e ITENS_PEDIDOS, ligando-as pelo campo PRODUTO_ID e outro JOIN com a tabela PEDIDOS, ligando-a pelo campo PEDIDO_ID. Aplica-se um filtro para considerar apenas os pedidos feitos no mês de dezembro, utilizando a função strftime para extrair o mês da data (%m) de compra e compará-lo com '12'.

Por fim, os dados são agrupados pelos produtos e ordenados em ordem decrescente com base na quantidade de vendas. Como retorno, temos uma tabela com a contagem de vendas de cada produto de todos os pedidos realizados em dezembro.

query = '''SELECT PRODUTOS.PRODUTO, COUNT(*) AS quantidade_vendas
FROM ITENS_PEDIDOS
JOIN produtos ON produtos.produto_id = ITENS_PEDIDOS.produto_id
JOIN PEDIDOS ON PEDIDOS.PEDIDO_ID = ITENS_PEDIDOS.PEDIDO_ID
WHERE strftime('%m',PEDIDOS.data_compra)= '12'
GROUP BY produtos.produto
ORDER BY quantidade_vendas DESC;
'''
sql_df(query)