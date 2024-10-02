**Faça Como Eu Fiz** = **Mão na Massa**

## Aula 1
### Preparando o ambiente  
Esse curso tem como objetivo a construção de um dashboard de vendas a partir de dados de uma API. Para realizar essa tarefa, serão utilizadas as seguintes bibliotecas:

Streamlit para a construção de um aplicativo web;
Requests para acessar dados da API;
Pandas para manipulação de dados;
Plotly para a elaboração de gráficos.
A IDE que vamos usar no curso é o Visual Studio Code. Dessa maneira, para preparar o nosso ambiente, começaremos com dois downloads: do interpretador Python e do VSCode.

Download do interpretador Python
Para realizar o download do interpretador Python, basta acessar a página de downloads do Python e selecionar a opção referente ao sistema operacional.

alt text: captura de tela da página de download do site da linguagem de programação Python. Há um botão amarelo "Download Python 3.10.7" abaixo do título da página "Download the latest version for Windows". Um retângulo vermelho dá destaque para a parte de seleção do download para outros sistemas operacionais: Windows, Linux/UNIX, macOS, Outros

Caso esteja utilizando o sistema operacional Linux, é possível instalar utilizando o comando:

sudo apt-get install Python3Copiar código
Download VSCode
Para baixar o Visual Studio Code, acesse a página inicial do software e selecione o botão de download de acordo com o sistema operacional utilizado.

alt text: captura de tela da página de download do site do programa Visual Studio Code. Há um botão azul "Download for Windows" e um ícone em destaque ao lado direito do botão em forma de V que dá acesso a uma lista suspensa. Nessa lista suspensa é possível visualizar botões de download para outros sistemas operacionais: macOS, Windows x64 e Linux x64. Essas opções estão destacadas com setas vermelhas.

Após o download e instalação, podemos abrir o VSCode e baixar a extensão do Python dentro dele. Para isso, podemos acessar o último ícone da barra lateral do VSCode e na barra de pesquisa digitar "Python". Logo a primeira extensão que aparecer podemos clicar em "Install":

alt text: captura de tela da barra de extensões do aplicativo VScode. Na lateral esquerda da tela existe uma barra de pesquisa com o texto "python". Abaixo dessa barra é apresentado o ícone do Python, que são duas cobrinhas, e a palavra "Python" logo à direita. O ícone e o texto encontram-se destacados por um mesmo retângulo vermelho.

## Aula 2
### Desafio: aba quantidade de vendas  
Nosso dashboard estava ficando bem carregado de informação e, para adicionar gráficos para expandir a análise dos dados, criamos novas abas usando o método st.tabs(). Essa é uma solução muito boa para segmentar os conteúdos no aplicativo e facilitar a navegação do usuário.

Em uma dessas abas, foi deixado o desafio de colocar gráficos relacionados a quantidade de vendas. Chegou o momento de praticar e resolver esse desafio, que pode ser dividido em 4 partes:

Construir um gráfico de mapa com a quantidade de vendas por estado.
Construir um gráfico de linhas com a quantidade de vendas mensal.
Construir um gráfico de barras com os 5 estados com maior quantidade de vendas.
Construir um gráfico de barras com a quantidade de vendas por categoria de produto.

### Opinião do instrutor  
Tabelas
Para resolver esse desafio, vamos primeiro construir as tabelas que servirão como fonte de dados para os gráficos, utilizando a biblioteca Pandas.

Tabela de quantidade de vendas por estado:

vendas_estados = pd.DataFrame(dados.groupby('Local da compra')['Preço'].count())
vendas_estados = dados.drop_duplicates(subset = 'Local da compra')[['Local da compra','lat', 'lon']].merge(vendas_estados, left_on = 'Local da compra', right_index = True).sort_values('Preço', ascending = False)Copiar código
Tabela de quantidade de vendas mensal:

vendas_mensal = pd.DataFrame(dados.set_index('Data da Compra').groupby(pd.Grouper(freq = 'M'))['Preço'].count()).reset_index()
vendas_mensal['Ano'] = vendas_mensal['Data da Compra'].dt.year
vendas_mensal['Mes'] = vendas_mensal['Data da Compra'].dt.month_name()Copiar código
Tabela de quantidade de vendas por categoria de produtos:

vendas_categorias = pd.DataFrame(dados.groupby('Categoria do Produto')['Preço'].count().sort_values(ascending = False))Copiar código
Gráficos
Agora, vamos criar os gráficos usando a biblioteca Plotly.

Gráfico de mapa de quantidade de vendas por estado:

fig_mapa_vendas = px.scatter_geo(vendas_estados, 
                     lat = 'lat', 
                     lon= 'lon', 
                     scope = 'south america', 
                     #fitbounds = 'locations', 
                     template='seaborn', 
                     size = 'Preço', 
                     hover_name ='Local da compra', 
                     hover_data = {'lat':False,'lon':False},
                     title = 'Vendas por estado',
                     )Copiar código
Gráfico de quantidade de vendas mensal:

fig_vendas_mensal = px.line(vendas_mensal, 
              x = 'Mes',
              y='Preço',
              markers = True, 
              range_y = (0,vendas_mensal.max()), 
              color = 'Ano', 
              line_dash = 'Ano',
              title = 'Quantidade de vendas mensal')

fig_vendas_mensal.update_layout(yaxis_title='Quantidade de vendas')Copiar código
Gráfico dos 5 estados com maior quantidade de vendas:

fig_vendas_estados = px.bar(vendas_estados.head(),
                             x ='Local da compra',
                             y = 'Preço',
                             text_auto = True,
                             title = 'Top 5 estados'
)

fig_vendas_estados.update_layout(yaxis_title='Quantidade de vendas')Copiar código
Gráfico da quantidade de vendas por categoria de produto:

fig_vendas_categorias = px.bar(vendas_categorias, 
                                text_auto = True,
                                title = 'Vendas por categoria')
fig_vendas_categorias.update_layout(showlegend=False, yaxis_title='Quantidade de vendas')Copiar código
Inserir elementos no Streamlit
Por fim, vamos inserir os elementos gráficos na 2ª aba do nosso aplicativo, referente a quantidade de vendas:

with aba2:
    coluna1, coluna2 = st.columns(2)
    with coluna1:
        st.metric('Receita', formatar_numero(dados['Preço'].sum(), 'R$'))
        st.plotly_chart(fig_mapa_vendas, use_container_width = True)
        st.plotly_chart(fig_vendas_estados, use_container_width = True)

    with coluna2:
        st.metric('Quantidade de vendas', formatar_numero(dados.shape[0]))
        st.plotly_chart(fig_vendas_mensal, use_container_width = True)
        st.plotly_chart(fig_vendas_categorias, use_container_width = True)Copiar código

## Aula 3
### Desafio: adicionando input widgets  
O Streamlit oferece diversas opções de elementos que aceitam o input do usuário e podem ser utilizados para deixar o aplicativo dinâmico. No nosso projeto, estamos utilizando esses elementos para a construção de filtros para os gráficos do dashboard e para a filtragem de um DataFrame.

Construímos elementos de input para filtrar os dados de 3 colunas do DataFrame e foi deixado um desafio de construir os filtros para as colunas restantes. Chegou o momento de praticar e resolver esse desafio. Como dica para solução, colunas com dados categóricos podem ser filtrados com o st.multiselect(), enquanto colunas com dados numéricos podem ser filtrados com o st.slider().

### Opinião do Instrutor  
Para solucionar esse desafio, precisamos identificar quais são as colunas com dados categóricos e quais possuem dados numéricos.

Coluna	Tipo de dado	Elemento Streamlit
Nome do produto	Categórico	st.multiselect
Categoria do produto	Categórico	st.multiselect
Preço	Numérico	st.slider
Frete	Numérico	st.slider
Data da Compra	Data	st.date_input
Vendedor	Categórico	st.multiselect
Local da Compra	Categórico	st.multiselect
Avaliação da compra	Numérico	st.slider
Tipo de pagamento	Categórico	st.multiselect
Quantidade de parcelas	Numérico	st.slider
As colunas de latitude e longitude não foram selecionadas como opções de filtros porque não são informações intuitivas e a região pode ser filtrada pela coluna 'Local da Compra'.

A partir da identificação do tipo de dado, basta utilizar o elemento do Streamlit correspondente, criando um st.expander para esconder o filtro caso não esteja sendo usado:

with st.sidebar.expander('Nome do produto'):
    produtos = st.multiselect('Selecione os produtos', dados['Produto'].unique(), dados['Produto'].unique())
with st.sidebar.expander('Categoria do produto'):
    categoria = st.multiselect('Selecione as categorias', dados['Categoria do Produto'].unique(), dados['Categoria do Produto'].unique())
with st.sidebar.expander('Preço do produto'):
    preco = st.slider('Selecione o preço', 0, 5000, (0,5000))
with st.sidebar.expander('Frete da venda'):
    frete = st.slider('Frete', 0,250, (0,250))
with st.sidebar.expander('Data da compra'):
    data_compra = st.date_input('Selecione a data', (dados['Data da Compra'].min(), dados['Data da Compra'].max()))
with st.sidebar.expander('Vendedor'):
    vendedores = st.multiselect('Selecione os vendedores', dados['Vendedor'].unique(), dados['Vendedor'].unique())
with st.sidebar.expander('Local da compra'):
    local_compra = st.multiselect('Selecione o local da compra', dados['Local da compra'].unique(), dados['Local da compra'].unique())
with st.sidebar.expander('Avaliação da compra'):
    avaliacao = st.slider('Selecione a avaliação da compra',1,5, value = (1,5))
with st.sidebar.expander('Tipo de pagamento'):
    tipo_pagamento = st.multiselect('Selecione o tipo de pagamento',dados['Tipo de pagamento'].unique(), dados['Tipo de pagamento'].unique())
with st.sidebar.expander('Quantidade de parcelas'):
    qtd_parcelas = st.slider('Selecione a quantidade de parcelas', 1, 24, (1,24))Copiar código


## Desafio: query de filtro
Depois de inserir os elementos de input do Streamlit, é o momento de usar a informação disponibilizada pelo usuário para filtrar o DataFrame usando a biblioteca Pandas. Para fazer a filtragem de todas as colunas de uma só vez, podemos usar o método query() com uma expressão booleana no formato de string.

Iniciamos a filtragem com a query de 3 colunas do DataFrame e foi deixado um desafio de construir a query para as colunas restantes. Chegou o momento de praticar e resolver esse desafio. Dicas para a solução:

observe o tipo de dado da coluna para identificar como escrever a expressão booleana;
coloque entre duas crases os nomes de colunas que contêm espaços;
use o @variavel para trabalhar com variáveis dentro da string.
### Opinião do Instrutor  
Para solucionar esse desafio, vamos construir dois tipos de expressão booleana:

colunas categóricas: `Nome coluna` in @variavel
colunas numéricas: @variavel[0] <= `Nome coluna` <= @variavel[1]
Essas expressões serão avaliadas uma a uma, e podemos avaliá-las em conjunto usando o operador and. Substituindo cada uma das colunas e as respectivas variáveis criadas a partir dos elementos de input do Streamlit, ficamos com o seguinte resultado para a query:

query = '''
Produto in @produtos and \
`Categoria do Produto` in @categoria and \
@preco[0] <= Preço <= @preco[1] and \
@frete[0] <= Frete <= @frete[1] and \
@data_compra[0] <= `Data da Compra` <= @data_compra[1] and \
Vendedor in @vendedores and \
`Local da compra` in @local_compra and \
@avaliacao[0]<= `Avaliação da compra` <= @avaliacao[1] and \
`Tipo de pagamento` in @tipo_pagamento and \
@qtd_parcelas[0] <= `Quantidade de parcelas` <= @qtd_parcelas[1]
'''