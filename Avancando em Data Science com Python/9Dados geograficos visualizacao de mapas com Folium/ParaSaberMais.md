# Para Saber Mais

## Aula 1

### Para saber mais: controle de camadas  
A biblioteca Folium permite a criação da visualização de mapas a partir de camadas. A primeira delas é a camada de fundo de mapa, que é composta por elementos essenciais em uma visualização cartográfica porque fornece o contexto geográfico para entender e analisar os dados que serão apresentados no mapa.

Por padrão, são disponibilizadas diversas camadas, que podem ser encontradas diretamente na [documentação da biblioteca](https://python-visualization.github.io/folium/latest/reference.html), na descrição do método Map():

OpenStreetMap
Mapbox Bright (Com níveis de zoom limitados)
CartoDB Positron
CartoDB Dark Matter
Além dos tipos de visualização padrão, podemos explorar [camadas personalizadas da Leaflet](https://leaflet-extras.github.io/leaflet-providers/preview/), que é uma biblioteca JavaScript usada para criar mapas interativos na internet e serve como base de construção do Folium.

Camadas de base podem ser criadas com o método folium.TileLayer() e adicionadas na visualização usando a função add_to(). Além disso, é possível alternar entre as visualizações de camadas de forma interativa, bastando criar um controle de camadas usando o método folium.LayerControl().  


## Aula 2
### Para saber mais: HeatMap ao longo do tempo   
Além da construção de um mapa de calor que identifica a concentração dos dados em um único momento, a biblioteca Foliumpermite construir mapas de calor animados, permitindo explorar e analisar a evolução temporal de dados geoespaciais. O nome do método capaz de realizar essa tarefa é o HeatMapWithTime.

Para utilizar o HeatMapWithTime, é necessário que o conjunto de dados possua coordenadas geográficas e informações de tempo associadas. A partir desses dados, é possível criar uma sequência de mapas de calor que se alternam de acordo com o tempo.

Funciona da seguinte maneira: para cada data ou período único do conjunto de dados, um mapa de calor é construído. Esses mapas de calor são então dispostos em ordem cronológica, criando assim uma animação onde é possível identificar períodos de maior ou menor concentração de dados, trazendo análises mais aprofundadas dos dados.

É uma ferramenta muito poderosa e muito prática. Ela possui as mesmas personalizações do mapa de calor convencional, além da possibilidade de ajustar a velocidade da animação, execução da animação automática e exibição do índice do período de cada mapa de calor, tudo isso através dos parâmetros do método HeatMapWithTime. Vale destacar que, assim como feito para a construção do HeatMap, é necessário realizar a importação a partir dos plugins do Folium:

from folium.plugins import HeatMapWithTime
Copiar código
Para entender o funcionamento, vamos a um exemplo com dados gerados aleatoriamente:

import folium
from folium.plugins import HeatMapWithTime
import numpy as np
from datetime import datetime, timedelta

np.random.seed(20)
dados_iniciais = np.random.normal(size=(100, 2)) * np.array([[0.03, 0.06]]) + np.array(
    [[-22.95, -43.3]]
)

dados = [(dados_iniciais + (np.random.normal(size=(100, 2)) * 0.01)).tolist() for i in range(20)]

data = [
    (datetime.now()- timedelta(20) + k * timedelta(1)).strftime("%Y-%m-%d") for k in range(20)
]
Copiar código
No código acima, as bibliotecas numpy e datetime foram importadas para gerar os dados aleatórios. Foram gerados 100 coordenadas de latitude e longitude nos dados_iniciais, centralizadas na latitude -22.95 e longitude -43.3, correspondendo à localização do Rio de Janeiro. A partir desses dados, foi gerada uma lista contendo 20 listas, cada uma com dados de latitude e longitude correspondendo a 20 períodos distintos. Após isso, foi gerada uma lista com as datas dos últimos 20 dias.

Esses dados simulam, por exemplo, os locais com a concentração de imóveis que foram vendidos nos últimos 20 dias. Com isso, cada um dos períodos irá exibir 100 imóveis distintos. Os dados precisam necessariamente estar nesse formato de lista de listas para que o método funcione corretamente. Agora, é possível representar isso em uma animação do Folium:

mapa = folium.Map([-22.95, -43.3], tiles="cartodbdark_matter", zoom_start=11)

HeatMapWithTime(dados, auto_play = True, index = data, speed_step=0.2).add_to(mapa)

mapa
Copiar código
Os parâmetros utilizados na função foram:

os dados, em formato de lista de listas, contendo as coordenadas de latitude e longitude dos 20 períodos;
auto_play para executar a animação automaticamente;
index para informar as datas dos períodos;
speed_step para modificar a velocidade da animação.
O resultado do código é o seguinte:

alt text: Gif com mapa de calor animado no município do Rio de Janeiro, mostrando pontos em 20 períodos distintos. Os pontos se movimentam a cada data, mostrando a alteração da latitude e longitude.

### Para saber mais: Tooltips  
Quando se trata de visualização de dados, precisamos tomar muito cuidado com a quantidade de informações que está sendo mostrada ao mesmo tempo para que o visual não fique muito carregado e transmita somente o necessário. Um visual interativo consegue trazer uma vantagem muito grande, porque a pessoa que está visualizando consegue selecionar a informação que está buscando a partir de botões ou outros elementos.

Uma ferramenta de interação muito útil e disponível na biblioteca Folium é o tooltip, que permite adicionar informações descritivas nos polígonos do mapa, fornecendo às pessoas usuárias detalhes adicionais sobre os elementos geográficos. O ponto-chave é que essas informações só serão exibidas quando o cursor do mouse for posicionado sobre o elemento visual do mapa, fazendo com que o visual não fique sobrecarregado e deixando a visualização de dados mais dinâmica.

O tooltip é bastante útil em conjuntos de dados mais complexos, que possuem muitas informações relevantes. Além disso, é possível personalizar a caixa de informação com formatação de texto, links e até mesmo imagens. Ele está disponível em diversas funcionalidades dentro do Folium, como marcadores, contornos de mapa e polígonos.

## Aula 3
### Para saber mais: marcadores circulares  
Além dos marcadores com ícones, é possível utilizar outros elementos visuais para representar informações em um mapa construído com o Folium. Um desses elementos é o círculo, que pode ser usado em um tamanho fixo para mostrar somente a localização, ou alterando o tamanho de acordo com uma informação numérica do conjunto de dados, transformando a visualização em um gráfico de bolhas.

Existem duas maneiras de construir círculos na biblioteca Folium: com o método folium.Circle ou com o método folium.CircleMarker. A diferença entre esses métodos está simplesmente no parâmetro radius que controla o tamanho do círculo. No primeiro método, o valor dado a esse parâmetro será um raio do círculo em metros. Já no segundo, o valor dado ao parâmetro controla o tamanho do raio em pixels na figura.

No projeto de análise da venda de imóveis, podemos dar um destaque aos imóveis que possuem uma área maior que os demais com um gráfico de bolhas, usando a informação da área como tamanho do círculo:

mapa_rio = folium.Map(location = [imoveis['Latitude'].mean(), imoveis['Longitude'].mean()],
                      zoom_start = 12,
                      tiles = 'cartodbpositron')

imoveis.apply(
    lambda linha: folium.Circle(
        location = [linha['Latitude'],
                    linha['Longitude']],
        color = 'black',
        fill_color = 'red',
        radius = linha['Area'],
        weight = 0.5,
        tooltip = f'Área: {linha["Area"]} m²'
    ).add_to(mapa_rio), axis = 1
)

mapa_rio
Copiar código
O resultado para o código acima pode ser visualizado abaixo:

alt text: Mapa de bolhas no município do Rio de Janeiro, com círculos de tamanhos distintos variando de acordo com a área de cada imóvel. Os círculos têm bordas em preto apresentam preenchimento em diferentes tonalidades de vermelho - os círculos maiores apresentam um vermelho mais claro, enquanto círculos menores apresentam o vermelho mais intenso e escuro. Há uma caixa de texto no centro informando que a área de um círculo selecionado é de 220 metros quadrados.

O código para criar o círculo é análogo ao folium.Marker, que foi visto durante o vídeo anterior. É necessário passar uma localização com latitude e longitude e existem parâmetros de personalização como a cor de borda e preenchimento. É possível até mesmo acrescentar tooltips para adicionar informações ao mover o cursor por cima do círculo.

Em resumo, tanto o folium.Circle quanto o folium.CircleMarker são ferramentas valiosas que permitem adicionar marcadores circulares personalizáveis em mapas interativos. São ótimas escolhas para visualização e análise de dados geoespaciais, permitindo que você crie mapas envolventes e informativos para suas necessidades.

### Para saber mais: ícones dos marcadores  
No momento de personalizar os marcadores que serão visualizados em um mapa, devemos ficar atentos para escolher ícones que sejam condizentes com o tipo de informação que queremos representar. O Folium permite a utilização de ícones através do método folium.Icon e, a partir dele, em um parâmetro com nome icon, selecionamos o tipo de ícone que será usado na formatação do marcador.

No nosso projeto, usamos o ícone de uma casa para representar os marcadores dos imóveis. Para isso, utilizamos no parâmetro icon, a string 'fa-home' e no parâmetro prefix, o prefixo 'fa'. Se quisermos representar um alfinete, podemos utilizar a string 'glyphicon-pushpin' com o prefixo 'glyphicon', conforme o exemplo de código:

mapa_rio = folium.Map(location = [imoveis['Latitude'].mean(), imoveis['Longitude'].mean()],
                      zoom_start = 10,
                      tiles = 'cartodbpositron')

amostra_imoveis = imoveis.sample(500)

amostra_imoveis.apply(
    lambda linha: folium.Marker(
        location = [linha['Latitude'],
                    linha['Longitude']],
        icon = folium.Icon(icon = 'fa-home', prefix = 'fa')
    ).add_to(mapa_rio), axis = 1
)

mapa_rio
Copiar código
O resultado para o código acima pode ser visualizado abaixo:

alt text: Mapa do município do Rio de Janeiro com marcadores azuis e com ícones de alfinete em branco representando imóveis à venda.

Os tipos de ícones que podem ser usados podem ser encontrados em dois sites:

[Font Awesome](https://lab.artlung.com/font-awesome-sample/)
[Bootstrap 3](https://getbootstrap.com/docs/3.3/components/)
A partir desses sites, podemos verificar a imagem do ícone, bem como o texto necessário para utilizar na função do Folium. Ao utilizar esses ícones, também é necessário informar o prefixo referente ao ícone em um parâmetro da função: devemos usar 'fa' quando o ícone utilizado for do site Font Awesome e 'glyphicon' quando o ícone utilizado for do site Bootstrap 3.

## Aula 4
### Para saber mais: Folium no GeoPandas  
A biblioteca Folium é bem completa, possuindo diversas funções e opções de personalização para cada uma delas. Isso permite criar visualizações únicas, que atendem todo tipo de demanda e projeto. Porém, caso o intuito do projeto seja mais simples ou não envolva uma visualização muito complexa e com muitas camadas, existe uma alternativa para criar uma visualização do Folium com apenas uma função a partir do GeoPandas.

A função em questão é a geopandas.GeoDataFrame.explore(), que gera um objeto de mapa do Folium a partir de um GeoDataFrame. Essa função possui diversos parâmetros para personalizar a visualização, oferecendo a opção de criar camadas, inserir tooltips, pop-ups e até mesmo criar mapas coropléticos. Algumas das funcionalidades vão exigir a importação da biblioteca mapclassify acima da versão 2.4, portanto, é recomendado instalar e importar a biblioteca para utilização da função:

!pip install mapclassify
import mapclassify
Copiar código
Essa é uma função bem completa, sendo desenvolvida para facilitar a exploração e análise de dados geoespaciais, e é capaz de gerar visualizações bem interessantes. Porém, por se tratar de apenas uma função e ser uma integração com a biblioteca Folium, ela não oferece todas as funcionalidades e, se o desejo for construir a melhor visualização possível, é necessário usar as funções específicas do Folium.

É possível usar a função explore() diretamente com os conjuntos de dados utilizados no curso, a exemplo no código abaixo:

base = bairros_rio.explore(tiles = 'Stamen Terrain', style_kwds = {'fillColor':'white','color':'black'})
amostra_imoveis = imoveis.sample(500)
amostra_imoveis.explore(m = base, tooltip = True, marker_type = 'marker') 
Copiar código
O código acima tem como resultado o seguinte mapa:

alt text: Mapa com os contornos dos bairros do Rio de Janeiro em preto e com marcadores azuis com um círculo interno branco representando imóveis à venda. Há uma caixa de texto com informações de um imóvel, como área em metros quadrados, bairro, quantidade de quartos, valor do imóvel, dentre outras informações.

Através do código, é possível ver como o método explore() simplifica a criação da visualização. Conseguimos personalizar o plano de fundo usando o parâmetro tiles e configurar a estilização do preenchimento e contorno com o style_kwds. Repare que não foi necessário a utilização de uma localização, isso foi detectado automaticamente a partir dos dados. Caso a base de dados possuísse as informações dos imóveis, poderíamos passar tudo dentro da mesma função, mas como não foi o caso, foi utilizada outra função explore(), a partir de uma amostra dos imóveis, onde foi possível acrescentar o tooltip de todas as colunas e selecionar um tipo de marcador.

Vale lembrar novamente que foi necessário instalar a biblioteca mapclassify antes de executar o código aqui mostrado. Caso queira saber mais sobre os parâmetros e formas de utilizar o método, veja a [documentação da função](https://geopandas.org/en/stable/docs/reference/api/geopandas.GeoDataFrame.explore.html) explore().

### Para saber mais: exportando a visualização  
O Google Colab ou outro ambiente de desenvolvimento é muito útil no momento de criação das visualizações, pois permite modificar o código e ver os resultados imediatamente até que a visualização fique completa. No entanto, o intuito de criar uma visualização é apresentá-la para outras pessoas, para ajudar na análise dos dados ou demonstrar uma visão das informações de um conjunto de dados. Para que isso seja possível, é necessário exportar essa visualização do ambiente de desenvolvimento e inserir em algum relatório, dashboard ou página da web.

O modo mais simples de executar isso é através do método save(), no qual a visualização é armazenada em um arquivo HTML. Esse arquivo pode ser aberto diretamente no navegador ou ainda utilizado em qualquer ferramenta que tenha integração com esse tipo de código de marcação. Dessa maneira, torna-se simples adicionar a visualização em websites e relatórios.

Caso o intuito seja criar um aplicativo totalmente interativo, uma ferramenta que é integrada ao Folium é a [Streamlit](https://streamlit.io/community). Ela permite a criação de gráficos de diversas bibliotecas, inclusive do Folium, a partir da função st_folium(). Para utilizar essa função, é necessário instalar um pacote a partir do código pip install streamlit-folium, criar a visualização usando as funções do Folium, e passar o objeto do mapa para a função st_folium.

Há uma documentação com diversas explicações de uso e exemplos práticos que pode ser acessado em um aplicativo criado pelo próprio Streamlit:

[Folium streamlit app](https://folium.streamlit.app/)
Se quiser saber mais sobre a ferramenta Streamlit, aqui na Alura também temos um curso que vai explorar a ferramenta a partir da construção de um dashboard interativo:

Streamlit: construindo um dashboard interativo