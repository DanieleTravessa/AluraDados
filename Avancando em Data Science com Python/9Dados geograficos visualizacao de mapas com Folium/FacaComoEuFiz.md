**Faça Como Eu Fiz** = **Mão na Massa**

## Aula 1
### Preparando o ambiente  
Neste curso, vamos utilizar a biblioteca [Folium](https://python-visualization.github.io/folium/latest/) para criar visualizações de dados de imóveis à venda no município do Rio de Janeiro. As visualizações serão mapas interativos que utilizam como fonte dados georreferenciados.

Instalação do GeoPandas
Atenção!
Para trabalhar com dados georreferenciados, será utilizada a biblioteca GeoPandas, em sua versão mais recente: 0.13.2. Para acompanhar o curso, é necessário instalar a GeoPandas, caso contrário, os códigos não serão executados e ocorrerão erros. Execute o código abaixo em uma célula do seu notebook de aula para instalar a biblioteca e conseguir executar os códigos do curso:

!pip install GeoPandas==0.13.2 
Copiar código
Dados georreferenciados
Os dados georreferenciados que iremos utilizar no projeto foram extraídos do site do [IBGE](https://www.ibge.gov.br/geociencias/downloads-geociencias.html?caminho=organizacao_do_territorio/malhas_territoriais/malhas_de_setores_censitarios__divisoes_intramunicipais/2021/Malha_de_setores_%28shp%29_por_UFs) e contêm os contornos dos setores censitários do estado do Rio de Janeiro. Você também pode realizar o download diretamente por aqui:

Base de dados: Malha censitária Rio de Janeiro
Vamos utilizar o [Google Colaboratory](https://colab.research.google.com/notebooks/welcome.ipynb) para construir o projeto. Para que você consiga usá-lo, é necessário ter uma conta Gmail, pois todo notebook ficará armazenado no Google Drive.


### Desafio: contornos dos subdistritos  
Os dados georreferenciados utilizados no curso possuem os contornos referentes a todos os setores censitários do estado do Rio de Janeiro. Isso traz um nível de detalhe muito grande, mas desnecessário para analisar dados de imóveis, visto que os setores são regiões muito pequenas e não tão conhecidas como os bairros da cidade, por exemplo.

A partir desses dados, foi possível extrair a informação dos contornos dos bairros e criar uma visualização utilizando o Folium. Na base de dados, há ainda uma informação dos subdistritos do município do Rio de Janeiro, regiões nomeadas que englobam vários bairros.

Como desafio, com base nessa coluna de subdistritos, realize as seguintes tarefas:

1 - Localize na base de dados a coluna com o nome dos subdistritos;

2 - Extraia a 'geometry' dos subdistritos a partir dos dados georreferenciados;

3 - Crie uma visualização dos contornos dos subdistritos usando o Folium.

Logo abaixo, na seção “Opinião da pessoa instrutora”, você encontra uma possível solução para o desafio.

### Opinião do instrutor
As tarefas desse desafio servem como um passo-a-passo para se chegar a visualização dos subdistritos.

Para encontrar o nome da coluna na base de dados, podemos utilizar os comandos cidade_rio.columns ou cidade_rio.head() para vasculhar as informações. As colunas são as seguintes:

['ID', 'CD_GEOCODI', 'TIPO', 'CD_GEOCODB', 'NM_BAIRRO', 'CD_GEOCODS',
       'NM_SUBDIST', 'CD_GEOCODD', 'NM_DISTRIT', 'CD_GEOCODM', 'NM_MUNICIP',
       'NM_MICRO', 'NM_MESO', 'geometry']
Copiar código
A coluna contendo o nome dos subdistritos é a 'NM_SUBDIST'. O próximo passo é realizar a extração dos contornos. Podemos fazer isso com o método dissolve() da biblioteca GeoPandas.

subdistritos_rio = cidade_rio.dissolve(by='NM_SUBDIST')
Copiar código
Agora que temos os contornos dos subdistritos, podemos gerar a visualização do mapa usando o Folium. Criamos a camada de base do mapa centralizada na latitude e longitude da região do Rio de Janeiro e adicionamos a camada de GeoJson dos subdistritos:

mapa_rio = folium.Map(
    location=[-22, -43],
    tiles="cartodbpositron",
    zoom_start=10,
)

folium.GeoJson(subdistritos_rio).add_to(mapa_rio)

mapa_rio

## Aula 2
### Dataset de imóveis
Nessa aula, vamos começar a analisar dados de imóveis à venda no município do Rio de Janeiro. Para isso, vamos utilizar um conjunto de dados contendo informações da localização de latitude e longitude, valor do imóvel, área em metros quadrados, entre outros dados.

Você pode realizar o download da base de dados a partir deste [link]().

## Aula 4
### Desafio: aplicando o aprendizado  
Durante o curso, foram criadas visualizações interativas usando dados de imóveis da cidade do Rio de Janeiro. Chegou a hora de praticar e aplicar o que foi aprendido com dados de imóveis da cidade de São Paulo.

Neste desafio, você deve carregar os dados do mapa e estatísticas de imóveis à venda na cidade de São Paulo. Você pode baixar as duas bases de dados a partir dos links:

Mapa da cidade de São Paulo
Estatísticas de imóveis
A partir desses dados, você deverá construir um mapa coroplético para representar a média de preço dos imóveis em cada distrito da cidade de São Paulo. Como um desafio adicional, insira tooltips para adicionar as estatísticas de quantidade de imóveis à venda e área em metros quadrados em cada um dos distritos.

### Opinião do instrutor  
Se desejar, você pode conferir a solução para o desafio no notebook Desafio do mapa de São Paulo.