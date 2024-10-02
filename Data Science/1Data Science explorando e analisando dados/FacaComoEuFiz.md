**Faça Como Eu Fiz** = **Mão na Massa**

## Aula 1
### Preparando o ambiente  
Neste curso, vamos analisar e explorar dados relativos a filmes e notas dos sites do [MovieLens](https://movielens.org/) e [TMDB](https://www.themoviedb.org/) (The Movie Database) utilizando a biblioteca [Pandas](https://pandas.pydata.org/pandas-docs/stable/) e gerar visualizações de dados, que dão suporte à análise, por meio da biblioteca [Seaborn](https://seaborn.pydata.org/tutorial/introduction).

Ambiente de trabalho
Utilizaremos uma ferramenta da Google chamada [Colaboratory](https://colab.research.google.com/notebooks/welcome.ipynb), que é similar ao [Jupyter Notebook](https://jupyter.org/). Para que você consiga utilizá-lo é necessário ter uma conta Gmail, pois todo notebook ficará armazenado no Google Drive.

Base de dados
Nesta primeira aula, vamos utilizar apenas o conjunto de dados do arquivo ratings.csv [no Github](https://raw.githubusercontent.com/alura-cursos/data-science-analise-exploratoria/main/Aula_0/ml-latest-small/ratings.csv).

Entretanto, podemos baixar as bases de dados que vamos utilizar no decorrer do curso a partir deste link. Caso queira, você também pode acessar o [GitHub do projeto](https://github.com/alura-cursos/data-science-analise-exploratoria/tree/main/Aula_0) para visualizar esses arquivos por lá.

Observação: Durante as aulas, vamos acessar cada base de dados por meio de seu link no GitHub para evitar a necessidade de fazer o upload dos arquivos a cada sessão.

Informações importantes sobre o Collaboratory
O código do seu notebook é executado em uma máquina virtual dedicada a sua conta. As máquinas virtuais são recicladas após um determinado tempo ocioso ou caso a janela seja fechada.

Para restaurar seu notebook, siga os seguintes passos no topo da página do Collaboratory: Ambiente de Execução → Reiniciar sessão e executar tudo.

 Discutir no Fórum


### Faça como eu fiz: conhecendo a base de notas dos filmes  
Vamos iniciar importando a biblioteca do Pandas e definindo o alias (apelido) como pd:

import pandas as pd
Copiar código
Na sequência, faremos a importação dos dados copiando e colando o link do GitHub com a base das notas e lendo os primeiros 5 primeiros valores:

notas = pd.read_csv("ratings.csv")
notas.head()
Copiar código
Analisando o DataFrame, percebemos que as colunas estão em inglês, o que dificulta a leitura. Então, vamos renomeá-las:

notas.columns = ["usuarioId", "filmeId", "nota", "momento"]
notas.head()
Copiar código
Vamos observar agora quais foram as notas possíveis da base de dados? Para isso vamos ler os dados únicos da coluna nota e, também, contaremos todas elas:

notas['nota'].unique()
notas['nota'].value_counts()
Copiar código
Agora, vamos criar o nosso primeiro visual utilizando a função plot() do pandas para observarmos a distribuição das notas dos usuários com um histograma:

notas["nota"].plot(kind='hist')
Copiar código
Vamos testar também outro visual, chamado boxplot, que também é uma forma de apresentar a descrição dos dados em um único visual:

import seaborn as sns
sns.boxplot(notas["nota"])
Copiar código
Pronto, agora é com você! Como podemos obter a média e mediana dos dados? E o resumo da descrição dos dados das notas dos usuários?

### Opinião do instrutor
Existem diversas formas de solucionar essa atividade. Apresentamos abaixo uma sugestão de solução para cada pergunta.

Podemos obter a média e a mediana da seguinte forma:

media = notas["nota"].mean()
mediana = notas["nota"].median()
print(f"Média é {media}")
print(f"Mediana é {mediana}")
Copiar código
Para descrever os dados das notas dos usuários podemos escrever o seguinte código:

notas["nota"].describe()
Copiar código
A prática é sempre muito importante para fixar o conteúdo. Ainda mais quando queremos progredir em nossas habilidades na exploração dos dados. Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é importante para o seu crescimento dentro da carreira de dados.

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.

## Aula 2
### Faça como eu fiz: analisando os dados dos filmes
Vamos iniciar fazendo uma nova importação dos dados, desta vez, copiando e colando o [link do GitHub](https://raw.githubusercontent.com/alura-cursos/data-science-analise-exploratoria/main/Aula_0/ml-latest-small/movies.csv) da base com o nome dos filmes separados pelo ID e os gêneros, alterando o nome das colunas e lendo os primeiros cinco valores:

filmes = pd.read_csv("https://raw.githubusercontent.com/alura-cursos/data-science-analise-exploratoria/main/Aula_0/ml-latest-small/movies.csv")
filmes.columns = ["filmeId", "titulo", "generos"]
filmes.head()
Copiar código
Desta base, vamos nos concentrar na análise dos 2 primeiros filmes “Toy Story” e “Jumanji” chamando-os por meio de seus IDs na base notas que criamos na aula anterior. Para isso, vamos ler a média das notas de cada um dos 2 filmes utilizando o método query():

notas.query("filmeId==1")["nota"].mean() # Média das notas de Toy Story
notas.query("filmeId==2")["nota"].mean()	 # Média das notas de Jumanji
Copiar código
Agora, vamos calcular média de todos filmes individualmente, agrupando-os por meio do método groupby() e utilizando como fórmula de agregação de dados o mean().

medias_por_filme = notas.groupby("filmeId")["nota"].mean()
medias_por_filme.head()
Copiar código
Vamos observar agora a distribuição das médias por filme? Criaremos um histograma e um boxplot, separadamente para esse processo:

medias_por_filme.plot(kind="hist")
Copiar código
sns.boxplot(medias_por_filme)
Copiar código
Por fim, para conseguirmos observar os dados que o boxplot apresenta, vamos ler o resumo dos dados com o describe().

medias_por_filme.describe()
Copiar código
Pronto, agora é com você! Como podemos criar um histograma das médias dos filmes com a biblioteca Seaborn? E adicionar um título em nosso visual?

## Aula 3
### Faça como eu fiz: explorando a nossa base dos filmes
Vamos importar uma nova base para nosso projeto, desta vez, copiando e colando o link do GitHub da base TMDB com uma série de filmes de diferentes línguas e com diversas características e lendo os primeiros cinco valores:

tmdb = pd.read_csv("https://raw.githubusercontent.com/alura-cursos/data-science-analise-exploratoria/main/Aula_0/tmdb_5000_movies.csv")
tmdb.head()
Copiar código
São muitos dados, não é mesmo? Vamos dar uma checada nos dados de receita (revenue) e orçamento (budget). Começando inicialmente com a distribuição das receitas dos filmes:

sns.displot(tmdb["revenue"])
plt.title("Distribuição da receita dos filmes")
plt.show()
Copiar código
Agora, vamos também gerar um novo gráfico para a distribuição do orçamento dos filmes. Para isso, podemos utilizar a IA dentro do Colab passando o seguinte prompt:

Gráfico de distribuição do orçamento dos filmes (budget)

É muito importante que você observe com cuidado como utilizá-la, sempre verificando se os códigos gerados fazem sentido e se os dados que você utiliza não são sensíveis. Vamos notar o resultado:

import matplotlib.pyplot as plt
sns.displot(tmdb["budget"])
plt.title("Distribuição do orçamento dos filmes")
plt.show()
Copiar código
Uma coisa interessante que podemos fazer para compreender os dados que estamos trabalhando é por meio da utilização do método info(), que traz um resumo de todas as colunas de nosso DataFrame. Com ele podemos saber a quantidade de registros e colunas, quantos dados não-nulos por coluna possuímos e o tipo dos dados:

tmdb.info()
Copiar código
Podemos observar durante a aula, uma grande quantidade de dados de receita com valor 0. Trataremos isso filtrando os dados só para receitas acima de 0 e recriaremos o histograma com a distribuição dos faturamentos:

com_faturamento = tmdb.query("revenue > 0")
sns.displot(com_faturamento["revenue"])
Copiar código
Por fim, visualizamos, respectivamente, as diferentes línguas originais dos filmes em um array e contamos quantas vezes cada uma aparece.

tmdb["original_language"].unique()
Copiar código
tmdb["original_language"].value_counts()
Copiar código
Pronto, agora é com você! Como podemos filtrar os dados para gerarmos um visual com a distribuição da média das notas do TMDB (vote_average) em que o número de votos (vote_count) seja maior que 10?  

### Opinião do instrutor  
Existem diversas formas de solucionar essa atividade. Apresentamos abaixo uma sugestão de solução.

Podemos criar o visual com a distribuição da média das notas do TMDB cujo número de votos seja maior que 10 da seguinte forma:

import matplotlib.pyplot as plt
mais_de_10_votos = tmdb.query("vote_count > 10")
sns.displot(mais_de_10_votos["vote_average"])
plt.title("Distribuição das médias das notas dos filmes\ncom mais de 10 votos")
plt.show()
Copiar código
A prática é sempre muito importante para fixar o conteúdo. Ainda mais quando queremos progredir em nossas habilidades na exploração dos dados. Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é importante para o seu crescimento dentro da carreira de dados.

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.  

## Aula 4  
### Faça como eu fiz: visualizando os dados da base  
Total dos idiomas
Com os dados do TMDB já importados, faremos uma avaliação de quantos idiomas existem em nosso arquivo .csv, primeiro efetuando a contagem dos valores e índices.

tmdb["original_language"].value_counts().index
tmdb["original_language"].value_counts().values
Copiar código
Em seguida, contaremos os valores da coluna original_language, transformando-os em um DataFrame, e reiniciaremos o índice da coluna. Vamos também mudar o nome das colunas para uma de fácil interpretação e exibir os 5 primeiros elementos:

contagem_de_lingua = tmdb["original_language"].value_counts().to_frame().reset_index()
contagem_de_lingua.columns = ["original_language", "total"]
contagem_de_lingua.head()
Copiar código
Com o Seaborn, iremos plotar alguns gráficos para trabalharmos a visualização desses dados. Vamos passar o original_language para o eixo x; total para o eixo y; e contagem_de_lingua como fonte dos dados:

sns.barplot(x="original_language", y = "total", data = contagem_de_lingua)
Copiar código
Também podemos criar um gráfico de barras com dados categóricos (categorias) com o countplot(), passando apenas a coluna com as categorias no eixo x ou y para que ele efetue a contagem dos elementos na coluna:

sns.countplot(data=tmdb, x="original_language")
Copiar código
Total dos idiomas exceto inglês (en)
Seguindo o contexto da aula com o dados do TMDB e a biblioteca do Seaborn importada, vamos agora verificar a quantidade de línguas que existem no nosso dataframe, exceto a língua inglesa.

Para isso, começaremos contando os valores das categorias (línguas) que existem no DataFrame. Em seguida, somamos esses valores, passando para a variável total_geral. Dessa variável, iremos subtrair somente os filmes cuja língua é inglês (en), resultando no nosso total_do_resto:

total_por_lingua = tmdb["original_language"].value_counts()
total_geral = total_por_lingua.sum()
total_de_ingles = total_por_lingua.loc["en"]
total_do_resto = total_geral - total_de_ingles
print(total_geral, total_de_ingles, total_do_resto)
Copiar código
Prosseguindo, criaremos um dicionário do Pandas contendo duas colunas: "lingua", dividida entre ingles e outros; e "total", com os valores de total_de_ingles e total_do_resto. Com esse dicionário, iremos gerar um DataFrame:

dados = {
  "lingua" : ["ingles", "outros"],
  "total" : [total_de_ingles, total_do_resto]
}
dados = pd.DataFrame(dados)
dados
Copiar código
Por fim, vamos criar, então, um gráfico de barras no qual o eixo x terão as línguas da base, e o y as ocorrências no conjunto:

sns.barplot(x="lingua", y="total", data = dados)
Copiar código
Analisando essas visualizações e lembrando dos conhecimentos adquiridos em aula, como podemos gerar um gráfico de pizza?  
### Opinião do instrutor  
Apresentamos abaixo uma sugestão de solução. Não deixe de tentar outras formas também, pratique bastante e boa sorte!

Vamos lá:

Para gerarmos um gráfico de pizza, optamos por utilizar o Matplotlib. Primeiro, importamos essa biblioteca com import matplotlib.pyplot as plt. Em seguida, instanciamos plt.pie(), passando como parâmetros nossos dados e os rótulos (labels).

A prática é sempre muito importante para fixar o conteúdo. Ainda mais quando queremos progredir em nossas habilidades na exploração dos dados. Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é importante para o seu crescimento dentro da carreira de dados.

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.  

## Aula 5  
### Faça como eu fiz: refinando o gráfico das línguas  
Vamos prosseguir para a criação de um novo visual. Para isso, criaremos uma nova variável total_de_outros_filmes_por_lingua, que receberá uma query() retornando todos os valores das categorias diferentes de en:

total_de_outros_filmes_por_lingua = tmdb.query("original_language != 'en'")["original_language"].value_counts()
total_de_outros_filmes_por_lingua.head()
Copiar código
Observamos os 5 valores mais frequentes logo acima. Agora, vamos construir um countplot() que receba a consulta de todos os filmes excetos em língua inglesa, passando a coluna original_language para a contagem de ocorrências:

sns.countplot(data=tmdb.query("original_language != 'en'"), x="original_language")
Copiar código
Pronto! Temos a primeira versão do visual ainda com os dados desordenados, mas conseguimos notar todas as línguas possíveis, exceto inglês, em um gráfico de barras. Vamos ordenar os dados e adicionar cores?

Para isso, utilizaremos 2 parâmetros no countplot():

order: como ordenar os dados. Aqui vamos ordenar de acordo com o índice em total_de_outros_filmes_por_lingua;
hue: determina qual coluna devemos utilizar para colorir o gráfico. Aqui, vamos passar o mesmo valor do eixo x original_language.
sns.countplot(data=tmdb.query("original_language != 'en'"),
              order=total_de_outros_filmes_por_lingua.index,
              hue="original_language",
              x="original_language")
Copiar código
Nada mal! Já conseguimos perceber a ordenação e notar diferentes cores nos gráficos, mas as cores não seguem um padrão que ajudariam a informar. Para isso, você pode acessar o [tutorial do Seaborn](https://seaborn.pydata.org/tutorial/color_palettes.html) com a escolha da paleta de cores e definir qual é o ideal para sua visualização.

Aqui utilizamos a “mako” para palette, que sai de um tom de azul mais escuro para um tom verde mais claro. Além disso, passamos para hue_order, responsável por ordenar as cores, a mesma ordenação dos dados (order) e ajustamos o tamanho da figura para (16, 8) pelo figsize do plt.figure().

plt.figure(figsize=(16, 8))
sns.countplot(data=tmdb.query("original_language != 'en'"),
              order=total_de_outros_filmes_por_lingua.index,
              palette="mako",
              hue="original_language",
              hue_order=total_de_outros_filmes_por_lingua.index,
              x="original_language")
Copiar código
Legal, né? E agora, como conseguimos alterar esse visual para ao invés de representar a frequência de ocorrência dos idiomas nos filmes nós contássemos a distribuição percentual dos idiomas exceto inglês? Coloque também um título no visual.

### Opinião do instrutor  
Existem diversas formas de solucionar essa atividade. Apresentamos abaixo uma sugestão de solução.

Podemos construir um gráfico com a distribuição percentual dos idiomas exceto inglês da seguinte forma:

plt.figure(figsize=(16, 8))
sns.countplot(data=tmdb.query("original_language != 'en'"),
              order=total_de_outros_filmes_por_lingua.index,
              palette="mako",
              hue="original_language",
              hue_order=total_de_outros_filmes_por_lingua.index,
              stat="percent",
              x="original_language")
plt.title("Distribuição da língua original nos filmes exceto em inglês")
plt.show()
Copiar código
A prática é sempre muito importante para fixar o conteúdo. Ainda mais quando queremos progredir em nossas habilidades na exploração dos dados. Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é importante para o seu crescimento dentro da carreira de dados.

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.  

## Aula 6  
### Faça como eu fiz: analisando distribuição com boxplot  
Vamos ler os primeiros 3 valores do DataFrame filmes que criamos na Aula 02 para ver quais médias iremos comparar

filmes.head(3)
Copiar código
De início iremos trabalhar com os 2 primeiros e faremos uma query para selecionar esses filmes, atribuindo suas notas às variáveis notas_do_toy_story e notas_do_jumanji. Vamos utilizar a IA para construir parte de nosso código por meio do seguinte prompt, alterando para o caso que desejamos aplicar:

Extraia as notas dos dois filmes em variáveis distintas

Em posse do código gerado pela IA e realizando as alterações necessárias temos o seguinte código:

notas_do_toy_story = notas.query("filmeId==1")["nota"]
notas_do_jumanji = notas.query("filmeId==2")["nota"]

media_do_toy_story = notas_do_toy_story.mean()
media_do_jumanji = notas_do_jumanji.mean()

print(media_do_toy_story, media_do_jumanji)
Copiar código
Fazendo o mesmo com a mediana, temos:

mediana_do_toy_story = notas_do_toy_story.median()
mediana_do_jumanji = notas_do_jumanji.median()

print(f"Média do Toy Story {media_do_toy_story}")
print("Mediana do Toy Story {mediana_do_toy_story }" )
print(f"Média do Jumanji {media_do_jumanji }")
print("Mediana do Jumanji {mediana_do_jumanji }" ) 
Copiar código
Para estudarmos mais profundamente a dispersão de dados, criaremos um exemplo hipotético com dois conjuntos de 20 notas cada um. O primeiro, filme1, contém um conjunto de 10 notas 2.5, e outro de 10 notas 3.5. Já o segundo, filme2, contém conjuntos de notas 5 e 1. Essas notas são agrupadas em arrays do Numpy. Importaremos esta biblioteca para utilizarmos aqui:

import numpy as np 
filme1 = [2.5] * 10 + [3.5] * 10
filme2 = [5] * 10 + [1] * 10
Copiar código
Mostraremos na tela as médias e as medianas das notas de ambos os filmes fictícios:

media_filme1 = np.mean(filme1)
mediana_filme1 = np.median(filme1)

media_filme2 = np.mean(filme2)
mediana_filme2 = np.median(filme2)

print("Filme 1:")
print("Média:", media_filme1)
print("Mediana:", mediana_filme1)

print("\nFilme 2:")
print("Média:", media_filme2)
print("Mediana:", mediana_filme2)
Copiar código
Vamos prosseguir exibindo os histogramas das notas dos dois filmes num mesmo visual e, em seguida, os boxplots para cada filme.

plt.hist(filme1)
plt.hist(filme2)

plt.boxplot([filme1, filme2])
Copiar código
Podemos perceber aqui, que por mais que as médias e as medianas coincidem, os dados estão espalhados de forma diferente. Para notar esse comportamento, vamos criar mais um filme fictício filme0 que recebe 20 notas 3.0, ou seja com média e mediana também 3, e vamos exibir os desvios padrões dos 3 filmes para perceber a suas diferenças:

filme0 = [3.0] * 20 
np.std(filme0), np.std(filme1), np.std(filme2)
Copiar código
Por fim, vamos criar o boxplot com as notas do Toy Story e Jumanji, tanto com Matplotlib quanto Seaborn, para verificar a mediana e o espalhamento das notas.

plt.boxplot([notas_do_toy_story, notas_do_jumanji])
Copiar código
sns.boxplot(data=notas.query("filmeId in [1,2]"), x="filmeId",  y="nota")
Copiar código
Dado esse exemplo, como podemos fazer um boxplot com as notas do Toy Story, do Jumanji e Grumpier Old Men, utilizando o Seaborn e o Matplotlib? Se possível adicione cores ao visual.  

### Opinião do instrutor  
Existem diversas formas de solucionar essa atividade. Apresentamos abaixo uma sugestão de solução para cada pergunta.

Primeiro, vamos criar a variável notas_do_grumpier_old_men com as notas do filme Grumpier Old Men e em seguida partir para a construção dos gráficos boxplot() com Matplotlib e Seaborn da seguinte forma:

notas_do_grumpier_old_men = notas.query("filmeId==3")["nota"]

# Boxplot com Matplotlib
plt.boxplot([notas_do_toy_story, notas_do_jumanji, notas_do_grumpier_old_men])
Copiar código
# Boxplot com Seaborn
sns.boxplot(data=notas.query("filmeId in [1,2,3]"), x="filmeId", y="nota", palette="Set2")
Copiar código
A prática é sempre muito importante para fixar o conteúdo. Ainda mais quando queremos progredir em nossas habilidades na exploração dos dados. Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é importante para o seu crescimento dentro da carreira de dados.

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.