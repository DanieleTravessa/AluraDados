**Faça Como Eu Fiz** = **Mão na Massa**

## Aula 1
### Preparando o ambiente  
Neste curso, vamos aprender técnicas de estilização de tabelas com foco em Data Visualization.

Antes de começar…
Para fazer este curso junto comigo, você vai precisar baixar o notebook do curso e fazer o upload dele no nosso ambiente de trabalho, o Google Colaboratory. Para que você consiga usar esse ambiente, é necessário ter uma conta Gmail, pois todo notebook ficará armazenado no Google Drive.

Além disso, iremos usar uma base de dados em formato csv, então, para construir o projeto junto comigo, você vai precisar baixar o arquivo relatorio_vendas.csv.


### Desafio: hora da prática
Vamos praticar o uso da visualização de tabelas através do Pandas. Para a prática, vamos utilizar outro conjunto de dados que está disponível para download: loja_livro_filmes.csv.

Nele, temos um relatório de custos de venda de livros e filmes de uma loja. Durante os desafios, a missão será trabalhar com os dados para fazer tabelas que podem se adequar a necessidade de diversas análises que podem ser feitas da loja. Para um melhor entendimento dos dados, abaixo está o que representa cada dado nas colunas.

pais: país de destino do produto.
id_cliente: código de identificação do cliente solicitante.
data_pedido: data de solicitação do produto por parte do cliente.
data_chegada: data de chegada do produto ao endereço de entrega informado pelo cliente.
tipo_compra: categoria que se enquadra a compra, podendo ser Normal ou Devolução.
numero_pedido: código de identificação da compra realizada.
tamanho_pacote: tamanho do pacote para envio do pedido.
unidades: quantidade de unidades compradas no pedido.
custo_empacotamento: valor do custo da loja para empacotar o produto.
custo_envio: valor do custo da loja para enviar o produto.
tipo_desconto: categoria do tipo de desconto aplicado.
categoria: categoria de tipo de produto.
tipo_consumo: nível de consumo do produto por tempo de uso.
tipo_cliente: categoria de tipo de cliente.
custo_produto: valor total do custo que o pedido resulta para a loja.
O primeiro desafio é construir uma visualização que permita identificar quais países mais solicitaram produtos por pedidos para que assim possa ser feito um estudo quanto a distribuição e logística de produtos.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Para te ajudar a verificar seus códigos, deixo disponibilizado um notebook para os desafios para você construir suas soluções. Você pode baixar ele e fazer o upload do notebook no Google Colab ou criar o seu próprio.

### Opinião do instrutor  
Podem existir diversas formas de solucionar uma questão. Irei apresentar como eu solucionei os problemas e não quer dizer que essa é a melhor solução, mas é uma opção de solução.

Para esse desafio construiremos uma tabela contendo um ranking dos 9 países que são vendidos os produtos, conforme a quantidade total de unidades vendidas.

## Importar o pandas e ler o arquivo
import pandas as pd
df = pd.read_csv('loja_livro_filmes.csv')

## Preparar os dados
# Agrupar a soma das unidades por pais e ordenar os valores
df_paises = df.groupby(['pais'])['unidades'].sum().nlargest(9).copy()
df_paises = df_paises.reset_index()

# Alterar os nomes das colunas e ajustar o ranqueamento
df_paises.columns = ['País', 'Unidades pedidas']
df_paises['Rank'] = df_paises.index + 1
df_paises.set_index('Rank', inplace=True)
df_paises

## Criar a visualização
s_pais = df_paises.style
# Formatar o texto para adicionar a unidade de medida
s_pais = s_pais.format({'Unidades pedidas': '{} prod'})
s_pais
copiar

## Aula 2
### Desafio: hora da prática
Aprendemos a construir uma visualização capaz de destacar elementos através de algumas funções built-in. E, nesse desafio, podemos aplicar algumas dessas funções.

O objetivo desse desafio é construir uma visualização que permita identificar quais categorias de produto geraram mais e menos custos para a loja.

Lembrando que, para dar continuidade ao desafio, você precisa ter feito o download do conjunto de dados loja_livro_filmes.csv. O dicionário de dados que descreve esse conjunto está disponível no desafio da aula 1.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Para te ajudar a verificar seus códigos, deixo disponibilizado um notebook para os desafios para você construir suas soluções. Você pode baixar ele e fazer o upload do notebook no Google Colab ou criar o seu próprio.
### Opinião do instrutor  
Podem existir diversas formas de solucionar uma questão. Irei apresentar como eu solucionei os problemas e não quer dizer que essa é a melhor solução, mas é uma opção de solução.

Por serem poucas categorias, apenas o uso das funções highlight_max e highlight_min é suficiente para destacar os produtos. Desse modo, vamos construir uma visualização que associa as categorias de produto com os custos totais gerados por pedido.

## Importar o pandas e ler o arquivo
import pandas as pd
df = pd.read_csv('loja_livro_filmes.csv')

## Preparar os dados
# Agrupar a soma dos custos dos pedidos por categoria
df_produto_custo = df.groupby(['categoria'])[['custo_produto']].sum()
# Ajustar o nome da coluna e index
df_produto_custo.index.name = 'Categoria produto'
df_produto_custo.columns = ['Custo de pedidos']
df_produto_custo

## Criar a visualização
s_produto = df_produto_custo.style
# Destacar elementos
s_produto.format('R$ {:,.2f}')\
         .highlight_max(color='#F16165')\
         .highlight_min(color='lightgreen')Copiar código


## Aula 3
### Desafio: hora da prática
Aprendemos a adicionar uma visualização gráfica na nossa tabela através da função bar. Nesse desafio, podemos aplicar essa função para treinarmos a construção da visualização com adição gráfica de uma forma bem similar ao que fizemos na aula.

O desafio é construir uma visualização que permita informar a quantidade e distribuição de pedidos por tipo de desconto. Isso irá permitir que os setores da empresa entendam a demanda de produtos em cada ação promocional.

Lembrando que, para dar continuidade ao desafio, você precisa ter feito o download do conjunto de dados loja_livro_filmes.csv. O dicionário de dados que descreve esse conjunto está disponível no desafio da aula 1.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Para te ajudar a verificar seus códigos, deixo disponibilizado um notebook para os desafios para você construir suas soluções. Você pode baixar ele e fazer o upload do notebook no Google Colab ou criar o seu próprio.

### Opinião do Instrutor  
Podem existir diversas formas de solucionar uma questão. Irei apresentar como eu solucionei os problemas e não quer dizer que essa é a melhor solução, mas é uma opção de solução.

É possível construir uma visualização similar à construída em aula. Portanto, seguirei passos similares para realizar esse desafio. Irei mudar apenas as propriedades do gráfico em barras.

## Importar o pandas e ler o arquivo
import pandas as pd
df = pd.read_csv('loja_livro_filmes.csv')

## Preparar os dados
# Ter o DataFrame fazendo a contagem dos pedidos em cada categoria de desconto
df_descontos = pd.DataFrame(df['tipo_desconto'].value_counts())
# Ajustar o nome da coluna e index
df_descontos.columns = ['N° pedidos']
df_descontos.index.name = 'Tipo desconto'
# Coletamos a distribuição da quantidade de pedidos por porcentagem
porcentagem = df_descontos['N° pedidos'].to_numpy()
porcentagem = 100 * porcentagem/porcentagem.sum()
df_descontos['Distribuição de pedidos'] = porcentagem
df_descontos

## Criar a visualização
s_descontos = df_descontos.style
# Utilizar propriedades CSS para formatar a visualização
cabecalho = {
    'selector': 'th',
    'props': 'font-weight: bold; font-family: Arial; text-align: right; background-color: white; color: black;'
}
celulas = {
    'selector': 'td',
    'props': 'background-color: white; color: black;'
}
s_descontos.set_table_styles([cabecalho, celulas], overwrite=False)
# Aplicar a visualização de gráfico
# os parâmetros height e width permitem alterar a proporção do tamanho do gráfico em relação a padrão 100
s_descontos.format({'Distribuição de pedidos': '{:.2f} %'})\
           .bar(subset='Distribuição de pedidos', vmin = 0, vmax = 100.0, color = '#093364',
                height=50,width=60)  


## Aula 4  
### Desafio: hora da prática
Durante a aula, aprendemos a lidar com muitos dados em uma tabela através da fixação de coluna pelo método set_sticky. Vamos lidar com muitos dados nesse desafio para podermos fixar o conteúdo aprendido.

Nosso desafio agora é fornecer uma visualização que permita mostrar o tempo médio de entrega de pedidos durante os meses dos anos de 2013 a 2015 por cada país. Isso vai permitir analisar o desempenho da parte de transportes da empresa durante os anos e traçar um planejamento de melhorias.

Lembrando que, para dar continuidade ao desafio, você precisa ter feito o download do conjunto de dados loja_livro_filmes.csv. O dicionário de dados que descreve esse conjunto está disponível no desafio da aula 1.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Para te ajudar a verificar seus códigos, deixo disponibilizado um notebook para os desafios para você construir suas soluções. Você pode baixar ele e fazer o upload do notebook no Google Colab ou criar o seu próprio.
### Opinião do Instrutor  
Podem existir diversas formas de solucionar uma questão. Irei apresentar como eu solucionei os problemas e não quer dizer que essa é a melhor solução, mas é uma opção de solução.

Nesse desafio, é interessante construir um novo DataFrame para adicionar colunas com novos dados, como uma coluna para datas no formato AAAA - MÊS e uma coluna para o tempo em dias de entrega.

Além disso, não podemos ter na visualização as informações datadas antes do ano de 2013, portanto é preciso fazer um filtro prévio dos dados.

## Importar o pandas e ler o arquivo
import pandas as pd
df = pd.read_csv('loja_livro_filmes.csv')

## Preparar os dados
# Tornar 'data_chegada' e 'data_pedido' colunas datetime
df['data_chegada'] = pd.to_datetime(df['data_chegada'])
df['data_pedido'] = pd.to_datetime(df['data_pedido'])

## Construir cópia de um DataFrame para adicionar novas colunas de dados
df_datas = df.copy()
df_datas = df_datas.sort_values('data_pedido')
df_datas = df_datas.reset_index(drop=True)

# Coletar apenas informações a partir do ano de 2013
df_datas = df_datas[df_datas['data_pedido'] >= '2013-01-01']

# Adicionar coluna com os meses formatados
df_datas['meses'] = df_datas['data_pedido'].dt.strftime('%Y - %b')

# Adicionar uma coluna com o tempo de entrega entre pedido e chegada
tempo_demora = (df_datas['data_chegada'] - df_datas['data_pedido']).dt.days
df_datas['tempo_entrega'] = tempo_demora

# Criar a estrutura em DataFrame
entregas = df_datas.pivot_table(index = 'pais', columns = 'meses', values = 'tempo_entrega' , aggfunc = 'mean', sort=False)

## Criar a visualização
s_entregas = entregas.style.format('{:,.2f}')
s_entregas.set_sticky(axis="index")Copiar código


## Aula 5
### Desafio: finalizando o projeto  
Durante o curso, foi feita uma tabela simplificada para um relatório de performance, mas ela não foi finalizada. O código da estilização pode ser observado abaixo:

# Criar estilização
compra_cliente = df_cliente.style.format('{:,.2f}')

# Criar uma visualização limpa
tabela = {
    'selector': 'td,th:not(.index_name)',
    'props': 'font-weight: normal; font-family: Arial; text-align: center; background-color: white'
}
index = {
    'selector': '.index_name',
    'props': 'font-weight: normal; text-align: right; font-style: italic; color: #696969'
}
compra_cliente.set_table_styles([tabela,index])

# Adicionar linhas
compra_cliente.set_table_styles({
    'Total': [{
        'selector':'th',
        'props': 'border-top: 1px solid #181818'
    },
    {
        'selector':'td',
        'props': 'border-top: 1px solid #181818'
    }],
    'B2B':[{
        'selector':'th',
        'props': 'border-top: 1px solid #181818'
    },
    {
        'selector':'td',
        'props': 'border-top: 1px solid #181818'
    }]
}, overwrite = False, axis=1)

# Selecionar e alterar o plano de fundo da célula com maior valor de Total
compra_cliente.set_table_styles({
    'Total': [{
        'selector': '.true',
        'props': 'background-color: #D8D8D8'
    }]
},overwrite=False,axis=0)

cores_coluna = pd.DataFrame(['false','true','false'],index= df_cliente['Total'].index,
                            columns = ['Total'])
compra_cliente.set_td_classes(cores_coluna)Copiar código
O desafio agora é finalizar a construção da tabela, destacando o elemento da linha Total. Você também pode aplicar outras estilizações que você achar mais adequadas à visualização.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

### Opinião do instrutor

Para selecionar a célula na linha Total, podemos seguir a mesma ideia de código apresentada na aula, com a diferença de que é preciso inverter os dados de linhas para colunas.

O primeiro passo é alterar o parâmetro axis para 1 no .set_table_styles, pois a seleção vai ser feita entre as colunas. Depois, na construção do seletor cores_linha, definimos a célula que será destacada através de uma lista de duas dimensões, pois os valores correspondem às colunas. Por fim, definimos as mesmas colunas do DataFrame df_cliente e o index como 'Total'. E com isso, aplicamos a seleção ao método .set_td_classes .

O código com a solução completa pode ser encontrado abaixo:

compra_cliente.set_table_styles({
    'Total': [{'selector': '.true', 'props': 'background-color: #D8D8D8;'}]
}, overwrite=False, axis=1)

cores_linha = pd.DataFrame([['false', 'false', 'true ', 'false', 'false']],
                            columns=df_cliente.columns,
                            index=['Total'])

compra_cliente.set_td_classes(cores_linha)

### Desafio: hora da prática  
No curso, aprendemos diversas formas para modificar nossa estilização, seja utilizando de funções built-in, seja criando estilos personalizados. [A documentação do Pandas](https://pandas.pydata.org/docs/user_guide/style.html#) traz um conjunto de recursos, explicações e exemplos de funções e métodos para estilização de tabelas e funciona muito bem como um complemento de estudos para explorar novas manipulações. Dito isso, vamos à nossa prática!

A empresa que estamos trabalhando distribui produtos por toda América do Sul para várias categorias de clientes. Nosso desafio envolve uma visualização que permita separar os gastos de envio de cada produto (custo total) por tipo de cliente, de modo que seja possível entender o tipo de produto que mais gerou custos de envio em cada tipo de cliente. Além disso, é interessante também mostrar a distribuição desses custos por país enviado, permitindo entender também os gastos por país.

Lembrando que, para dar continuidade ao desafio, você precisa ter feito o download do conjunto de dados loja_livro_filmes.csv. O dicionário de dados que descreve esse conjunto está disponível no desafio da aula 1.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Para te ajudar a verificar seus códigos, deixo disponibilizado um notebook para os desafios para você construir suas soluções. Você pode baixar ele e fazer o upload do notebook no Google Colab ou criar o seu próprio.
### Opinião do instrutor

Podem existir diversas formas de solucionar uma questão. Irei apresentar como eu solucionei os problemas e não quer dizer que essa é a melhor solução, mas é uma opção de solução. Deixo também disponibilizado o meu notebook com as soluções ou caso prefira uma visualização disponibilizo o link no [Github](https://github.com/alura-cursos/DV-estilizacao-tabelas/blob/main/Atividade%20de%20desafio/Solucao/desafio_solucao.ipynb).

Para a solução do desafio, realizei o agrupamento do tipo de cliente por tipo de compra e apliquei a separação dos custos de envio de produto por países. Na visualização, busquei adicionar uma coluna com total para destacar o tipo de produto que mais gerou custos de envio em cada tipo de cliente.

O desenvolvimento e descrição do código pode ser observado abaixo:

## Importar o pandas e ler o arquivo
import pandas as pd
df = pd.read_csv('loja_livro_filmes.csv')

## Preparar os dados

# Criar um DataFrame alternativo para ter um nome de coluna coerente com a visualização
df_alteracao = df.rename(columns={'pais': 'Custo por país ($)'})

# Agrupar os dados de tipo de cliente, com a categoria de produtos e os países que esses clientes importam o produto
df_clientes = df_alteracao.pivot_table(index=['tipo_cliente', 'categoria'], columns = 'Custo por país ($)', values = 'custo_produto', aggfunc = 'sum')

# Renomear o cabeçalho para nomes mais coerentes
df_clientes.rename_axis(index={'tipo_cliente': 'Tipo cliente', 'categoria': 'Categoria produto'}, inplace = True)

# Adicionar uma coluna que mostra a soma dos custos por tipo de cliente e categoria de produto
df_clientes['Total ($)'] = df_clientes.sum(axis=1)

## Criar a visualização
s_clientes = df_clientes.style.format('{:,.2f}')

# Criar os estilos base para a tabela, a partir da padronização das fontes, plano de fundo para branco e o alinhamento do cabeçalho para o topo
tabela = {
    'selector': 'td, th',
    'props': 'font-weight: normal; font-family: Arial; text-align: right; background-color: white;'
}
# Alinhar verticalmente o cabeçalho para o topo permite a pessoa observadora identificar onde começa a hierarquização dos grupos B2B e B2C
cabecalho = {
    'selector': 'th',
    'props': 'vertical-align: top'
}
s_clientes.set_table_styles([tabela, cabecalho])

# Adicionar linha de separação do cabeçalho superior
# Destacar as categorias que mais geraram custo com a aplicação de negrito nas fontes
s_clientes.set_table_styles({
    ('B2B', 'BlueRay'): [{'selector': 'th', 'props': 'border-top: 1px solid #181818'},
              {'selector': 'td', 'props': 'border-top: 1px solid #181818'}],
    ('B2B', 'Livro'): [{'selector': 'th', 'props': 'font-weight: bold'}],
    ('B2C', 'Livro'): [{'selector': 'th', 'props': 'font-weight: bold'}],
}, overwrite=False, axis=1)

# Destacar os elementos em cada tipo de cliente que mais geraram custos com uma seleção
s_clientes.set_table_styles({
    'Total ($)': [{
        'selector': '.true',
        'props': 'font-weight: bold'
    }]
},overwrite=False,axis=0)

cores_coluna = pd.DataFrame(['false','false','false','true','false','false','false','true'],index= df_clientes['Total ($)'].index,
                            columns = ['Total ($)'])
# Visualização final
s_clientes.set_td_classes(cores_coluna)Copiar código
 Discutir 