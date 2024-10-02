# Para Saber Mais

## Aula 1

### Para saber mais: o que o plano cartesiano tem a ver com visualização de dados?  
Mayza é uma estudante de Data Science em busca de novos conhecimentos e experiências. Em seu projeto mais recente, ela se deparou com um desafio: como criar gráficos em Python que realmente transmitam as informações necessárias? Com a mente inquieta e sedenta por respostas, ela está trabalhando em um projeto que requer a visualização de dados, porém não tem ideia de como pode começar. Ao mergulhar nos seus estudos, Mayza se deparou frequentemente com o termo plano cartesiano.

Você certamente já ouviu falar sobre esse termo. Pode ser que tenha sido em alguma aula de geografia, por exemplo. Mas afinal, o que isso tem a ver com a visualização de dados?

Imagine um mapa comum, daqueles que mostram ruas, pontos turísticos e outras informações úteis para quem está viajando. Seu objetivo principal é fornecer orientações e referências de forma clara e fácil de entender, a ponto de auxiliar o viajante a encontrar o caminho certo e tomar as melhores decisões durante sua jornada. O plano cartesiano segue a mesma ideia, porém ao invés de ruas e prédios, ele mostra informações em forma de gráficos. Com ele, podemos visualizar informações complexas de maneira intuitiva e eficiente, facilitando a tomada de decisões e a resolução de problemas por conta dos eixos que se cruzam em um ponto central.

Com o uso do plano cartesiano, constituído pelos eixo X e o eixo Y, é possível criar um sistema de coordenadas bidimensional que facilita a localização e análise de dados. Esses eixos também são conhecidos pelos seguintes nomes:

eixo x: eixo das abscissas.
eixo y: eixo das ordenadas.
Os eixos são componentes essenciais devido às suas combinações, que possibilitam uma maior precisão na identificação de pontos em um espaço bidimensional. Na figura abaixo, temos a representação de um plano cartesiano contendo os eixos X e Y para exemplificar. Com ele podemos notar algumas características importantes:

O eixo X é horizontal.
O eixo Y é vertical.
No centro temos a origem, o valor 0 (zero).
Para a direita e para cima temos valores positivos.
Para a esquerda e para baixo temos valores negativos.
Alt text: Representação de um plano cartesiano, contendo os eixos X e Y.

Como é possível constatar através dessas representações, os eixos nos permitem especificar a localização exata de um ponto em um espaço bidimensional, de modo que os valores de X e Y são chamados de coordenadas por descrevem a localização do ponto em relação à origem. Na figura abaixo, temos um plano cartesiano contendo pontos de algumas coordenadas: (2,5), (1,2), (0,-1), (-1,-4) e (-2,-7). Considere a representação e observe os pontos disponibilizados. Assim você pode visualizar melhor a relação entre eles e entender padrões e tendências nos dados.

Alt text: Representação de um plano cartesiano, contendo os eixos X e Y e algumas coordenadas: (2,5), (1,2), (0,-1), (-1,-4) e (-2,-7).

Quando nós criamos um gráfico, as coordenadas dos pontos são utilizadas para definir a posição de cada ponto no gráfico. E uma curiosidade interessante: o plano cartesiano e o eixo de coordenadas são amplamente usados em vários campos, incluindo Matemática, Física, Engenharia, Ciência de Dados e muitos outros, sendo uma ferramenta fundamental para a representação de dados e para a visualização de resultados em diversos contextos.

Você lembra da saga da Mayza? Depois de explorar as possibilidades em seus estudos, Mayza compreendeu o conceito de plano cartesiano e como isso pode ser útil no projeto de visualização de dados dela. Agora ela precisa de alguns insights para criar um gráfico e soube que você pode ajudá-la nisso.

E aí, vamos criar nosso primeiro gráfico agora?!
  
## Aula 2
### Para saber mais: boas práticas de visualização de dados para subplots

AJuliana, uma talentosa cientista de dados, decidiu mergulhar em um intrigante projeto no universo do varejo. Com seu conhecimento, e através de sua análise de dados, ela tem investigado as vendas mensais de diferentes produtos em várias lojas da empresa. Com o objetivo de entender melhor esses dados, ela decidiu criar um conjunto de subplots para comparar as vendas de diferentes produtos em cada loja.

Porém, no decorrer da criação desses subplots, Juliana pode notar a importância de seguir algumas boas práticas de visualização de dados para criar subplots eficazes e assim garantir que a figura resultante fosse clara e fácil de entender. Aqui estão algumas dicas que ajudaram Juliana a tornar sua figura mais detalhada e informativa:

Usar títulos claros e concisos: o título de cada subplot deve ser curto e descritivo para que o(a) leitor(a) possa rapidamente entender o que está sendo mostrado em cada um elemento. Além disso, se você estiver comparando diferentes conjuntos de dados, pode ser útil adicionar um subtítulo explicando o que está sendo comparado.

Manter a mesma escala nos eixos: para evitar distorções na comparação entre os subplots, é importante manter a mesma escala nos eixos X e Y em todos eles. Isso pode ser feito utilizando as funções set_xlim() e set_ylim().

Evitar sobrepor gráficos: é importante garantir que cada subplot seja claramente separado dos outros, sem sobreposição. Se houver uma sobreposição, a figura pode se tornar confusa e difícil de entender. Uma maneira de evitar sobreposições é ajustar o tamanho dos subplots para que haja espaço suficiente entre eles. Além disso, podemos adicionar a função fig.subplots_adjust() que recebe o parâmetro hspace. Ela controla o espaçamento vertical entre os subplots e o parâmetro wspace, que controla o espaçamento horizontal. O valor padrão desses parâmetros é 0.2, mas você pode ajustá-los de acordo com as suas necessidades.

Lembre-se que o valor passado para esses parâmetros é um número decimal que representa a fração do tamanho da figura, por exemplo, 0.5 significa que o espaçamento será de 50% da altura/largura da figura.

Com essas boas práticas em mente, Juliana criou seus subplots e conseguiu visualizar as vendas diárias de diferentes produtos de forma clara e eficaz em várias lojas da empresa. Ela foi capaz de identificar padrões interessantes nos dados e usou essas informações para fazer recomendações úteis para a empresa, nos deixando insights valiosos sobre boas práticas de visualização de dados para subplots.

Que tal impulsionar a qualidade e o impacto das suas visualizações colocando em prática essas valiosas dicas?! Explore e experimente todas essas possibilidades. Essa iniciativa, sem dúvida alguma, fará toda a diferença no seu desenvolvimento.  

## Aula 03
### Para saber mais: alterando estilos
Nós personalizamos as visualizações no vídeo anterior, alterando o tamanho das fontes, mudando a posição do título e também adicionando elementos como marcadores e grades às figuras. Mas além disso, segundo a documentação da biblioteca Matplotlib podemos aplicar diferentes estilos para permitir que nós adaptemos as visualizações de acordo com as nossas necessidades. Para saber quais estilos estão disponíveis, podemos imprimir style.available, onde style é um submódulo da biblioteca Matplotlib utilizado para definir estilos de visualização:

print(plt.style.available)Copiar código
O resultado é uma lista contendo todos os estilos disponíveis:

['Solarize_Light2', '_classic_test_patch', '_mpl-gallery', '_mpl-gallery-nogrid', 'bmh', 'classic', 'dark_background', 'fast', 'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn-v0_8', 'seaborn-v0_8-bright', 'seaborn-v0_8-colorblind', 'seaborn-v0_8-dark', 'seaborn-v0_8-dark-palette', 'seaborn-v0_8-darkgrid', 'seaborn-v0_8-deep', 'seaborn-v0_8-muted', 'seaborn-v0_8-notebook', 'seaborn-v0_8-paper', 'seaborn-v0_8-pastel', 'seaborn-v0_8-poster', 'seaborn-v0_8-talk', 'seaborn-v0_8-ticks', 'seaborn-v0_8-white', 'seaborn-v0_8-whitegrid', 'tableau-colorblind10']Copiar código
Podemos explorar um desses estilos para melhorar ainda mais nossas visualizações!

Antes de aplicar um estilo, é importante saber que cada vez que a biblioteca Matplotlib é importada em um notebook, ela define uma configuração de tempo de execução que inclui os estilos padrão para cada elemento de plotagem criado.

Portanto, para evitar que o estilo seja aplicado a todos os gráficos plotados no mesmo notebook, podemos utilizar um código que cria uma cópia das configurações padrão de plotagem da biblioteca Matplotlib e as atribui à variável IPython_default. Isso pode ser útil para armazenar e reutilizar as configurações padrão de plotagem ou para restaurá-las depois de terem sido modificadas:

IPython_default = plt.rcParams.copy()Copiar código
Um dos estilos disponíveis é baseado em um site de notícias e análises de dados chamado FiveThirtyEight, que cobre assuntos como política, economia, cultura, ciência e esportes.

Para utilizar o estilo 'fivethirtyeight' usamos o código abaixo:

plt.style.use('fivethirtyeight')Copiar código
Em seguida, podemos criar a figura, que terá esse novo estilo incorporado:

fig, ax = plt.subplots(figsize=(8, 4))
ax.plot(dados_brasil['ano'], dados_brasil['imigrantes'])
ax.set_title('Imigração do Brasil para o Canadá\n1980 a 2013', fontsize=20, loc='left')
ax.set_ylabel('Número de imigrantes', fontsize=14)
ax.set_xlabel('Ano', fontsize=14)
ax.yaxis.set_tick_params(labelsize=12)
ax.xaxis.set_tick_params(labelsize=12)
ax.xaxis.set_major_locator(plt.MultipleLocator(5))
plt.show()Copiar código
O resultado será o gráfico exibido abaixo:

Alt text: Figura obtida com o código anterior, utilizando o estilo fivethirtyeight.

Os gráficos criados com o estilo FiveThirtyEight são lindos e possuem estética limpa e minimalista, com linhas mais grossas e cores vibrantes.

Bom, mas e se a gente quiser plotar gráficos sem esse estilo depois de ter definido ele no notebook? Podemos redefinir os parâmetros utilizando rcParams.update e passando a ele a variável IPython_default que criamos anteriormente com as configurações padrão:

plt.rcParams.update(IPython_default);Copiar código
Além disso, podemos aplicar um estilo apenas a um bloco de código específico, pois o pacote de estilo fornece um gerenciador de contexto para limitar suas alterações a um escopo específico. Para isolar suas alterações de estilo, você pode escrever o código dentro de um contexto with da seguinte forma:

with plt.style.context('fivethirtyeight'):
  fig, ax = plt.subplots(figsize=(8, 4))
  ax.plot(dados_brasil['ano'], dados_brasil['imigrantes'], lw=3)
  ax.set_title('Imigração do Brasil para o Canadá\n1980 a 2013', fontsize=20, loc='left')
  ax.set_ylabel('Número de imigrantes', fontsize=14)
  ax.set_xlabel('Ano', fontsize=14)
  ax.yaxis.set_tick_params(labelsize=12)
  ax.xaxis.set_tick_params(labelsize=12)
  ax.xaxis.set_major_locator(plt.MultipleLocator(5))
  plt.show()Copiar código
Gostou desse novo estilo? A biblioteca Matplotlib oferece uma variedade de estilos, além do FiveThirtyEight, que podemos testar e aplicar aos nossos dados. Com essas opções, podemos tornar nossas visualizações ainda mais atraentes, melhorando a apresentação das informações que queremos transmitir.



## Aula 4  
### Para saber mais: como as cores podem tornar seus dados mais compreensíveis    

As cores podem ser um elemento poderoso para tornar seus dados mais compreensíveis e eficazes na comunicação de insights. A escolha das cores pode ser um fator crucial para o sucesso de um gráfico, pois elas podem ajudar a destacar informações importantes e atrair a atenção do público.

A biblioteca Seaborn oferece diversas paletas de cores, que são combinações pré-definidas de cores que podem ser usadas em seus gráficos. Essas paletas são projetadas para serem visualmente atraentes e para garantir que as cores usadas sejam facilmente distinguíveis entre si, no caso das paletas categóricas. Porém, a escolha da paleta mais adequada pode ser um desafio, pois depende do contexto e do objetivo da visualização. Por conta disso, podemos considerar que é possível criar gráficos mais interessantes e atraentes ao escolher as cores certas.

Ao escolher uma paleta de cores para o seu gráfico, é interessante considerar até mesmo as emoções que desejam ser transmitidas ao espectador. Cores podem despertar, por exemplo, sentimentos de tranquilidade, entusiasmo, seriedade e muito mais. Portanto, selecione cuidadosamente as cores que ajudarão a transmitir a mensagem desejada e criar a atmosfera adequada para o seu gráfico..

Para ajudar nesse processo, siga algumas dicas na hora de escolher as cores:

1 - Considerar o tipo de dado que está sendo plotado: dados categóricos, dados sequenciais ou dados divergentes requerem diferentes tipos de paletas de cores, como discutimos no vídeo anterior.

2 - Escolha cores que sejam facilmente distinguíveis umas das outras, se você estiver usando várias séries de dados em um único gráfico.

3 - Evite cores muito brilhantes e saturadas, pois podem ser muito intensas e distrair a atenção do público.

4 - Use cores de maneira consistente em todos os seus gráficos para facilitar a comparação entre eles.

5 - Considere o contexto em que o gráfico será utilizado e se as cores escolhidas são apropriadas para esse contexto.

Como mencionado anteriormente, uma importante capacidade das cores está em despertar diferentes reações nas pessoas que as observam. Para ilustrar isso, perceba o ambiente ao seu redor: cores como verde são geralmente associadas a sentimentos positivos, como alegria, esperança, crescimento e saúde. Portanto, essas cores são geralmente usadas para destacar informações positivas ou indicar que algo está indo bem. Por outro lado, cores mais escuras como o vermelho e o preto, podem ter conotações negativas e ser utilizadas para chamar a atenção para informações críticas ou problemáticas.

Um Olhar Para a Acessibilidade
Algo que devemos levar em consideração na hora de criarmos visualizações de dados é a experiência das pessoas usuárias. O que queremos dizer com isso? Devemos ter atenção nas cores e no tamanho das fontes que utilizamos, para que tenhamos uma visualização fácil e acessível para o nosso público.

Um ponto recorrente de adaptação que devemos levar em consideração nos nossos gráficos é aquele que beneficiará as pessoas com daltonismo, que possuem dificuldade de distinguir certas cores. Inclusive, existem ferramentas on-line que podemos utilizar para testar se nossos gráficos serão bem compreendidos por pessoas com daltonismo.

Um bom site para checar as cores das nossas imagens é o Coblis - Color Blindness Simulator. Nesta página você pode fazer upload das suas imagens e visualizar como as cores são vistas em diferentes tipos de daltonismo.

Atenção: Esse é um tema extenso que merece sempre atenção na hora de realizarmos nossas visualizações de dados para um público diverso. Por isso, é recomendável escolher cores que tenham contraste suficiente e que sejam facilmente distinguíveis entre si.

Por fim, é importante lembrar que a escolha das cores não deve substituir a qualidade dos dados e da análise. As cores devem ser usadas para complementar as informações apresentadas no gráfico, não para distrair ou confundir o nosso público-alvo. Portanto, vale à pena investir tempo na análise dos dados e na escolha das cores para garantir que o gráfico seja eficaz e fácil de entender. Dessa forma, você pode garantir uma experiência positiva e eficaz na comunicação dos seus dados por meio das visualizações.  

## Aula 5
### Para saber mais: animando gráficos para mostrar mudanças ao longo do tempo  
Nós aprendemos como criar gráficos interativos com a biblioteca Plotly, porém você sabia que é possível ir além e criar animações com essa mesma biblioteca? Além de tornar nossos gráficos mais interativos, as animações podem trazer ainda mais dinamismo e criatividade para as nossas visualizações.

Para ilustrar essa ideia, dê uma olhada na captura de tela de um notebook onde criei uma animação com os dados de imigração do Brasil para o Canadá. O código que gera essa animação começa exibindo a figura sem nenhuma linha. Ao clicar no botão "Play", no canto superior esquerdo da figura, a linha começa a surgir no primeiro tick do eixo X, que corresponde ao ano 1980, e vai se movendo até chegar ao final do eixo X, mostrando a evolução dos dados ao longo do tempo:

Captura da tela do Google Colab mostrando a figura gerada com a biblioteca Plotly com animação.

Com isso, podemos notar que a animação é uma ótima maneira de visualizar dados em evolução ao longo do tempo.

Você pode estar se perguntando: como podemos criar uma animação como essa? Fique tranquilo(a), estou aqui para te mostrar o caminho. Vou te explicar passo a passo!

1 - A primeira etapa após obter o DataFrame apenas com os dados do Brasil, como fizemos no começo do curso, é mudar o tipo de dados da coluna que contém os anos para int ao invés de manter como strings:

dados_brasil['ano'] = dados_brasil['ano'].astype(int)Copiar código
2 - Depois disso, vamos criar um bloco de código onde vamos construir essa animação, importando plotly.graph_objs, um módulo da biblioteca Plotly que contém classes para criar visualizações de dados interativas e personalizadas.

import plotly.graph_objs as goCopiar código
3 - Em seguida, uma figura vazia é criada usando a função go.Figure() e atribuída à variável fig.

fig = go.Figure()Copiar código
4 - A seguir, uma linha é adicionada ao gráfico usando a função fig.add_trace(). Nesta função, é passado um objeto Scatter, que recebe como argumentos os dados para os eixos X e Y do gráfico. Para que o gráfico seja exibido sem linha antes de clicar no botão play usamos o iloc[0] nas duas variáveis. Isso ocorre porque o iloc[0] seleciona o primeiro valor das colunas ano e imigrantes dos dados do Brasil, respectivamente. Ao adicionar esse ponto de dados à visualização do gráfico, ele será exibido inicialmente como um único ponto, sem linhas que o conectem a outros pontos.Além disso, passamos o modo de exibição lines, que quer dizer linhas e o nome da linha. Também é definida a espessura da linha usando o dicionário line=dict(width=4).

fig.add_trace(
    go.Scatter(x=[dados_brasil['ano'].iloc[0]], y=[dados_brasil['imigrantes'].iloc[0]], mode='lines', name='Imigrantes', line=dict(width=4))
)Copiar código
5 - Depois disso, o título do gráfico e as configurações do eixo X e Y são definidas usando a função fig.update_layout(). Os argumentos do título são:

text='<b>Imigração do Brasil para o Canadá no período de 1980 a 2013</b>': define o texto do título como uma string formatada em negrito (usando as tags HTML "<b>" e "</b>")
x=0.12: define a posição horizontal do título no layout, em relação à largura da figura. O valor 0.12 especifica que o título começará a 12% da largura da figura.
xanchor='left': define o alinhamento horizontal do título. O valor 'left' significa que o título será alinhado à esquerda do layout.
font=dict(size=20): define o tamanho do texto do título.
Já Os argumentos para xaxis e yaxis são dicionários, com as seguintes propriedades:

range=[1980, 2013]: define o intervalo do eixo, ou seja, o menor e o maior valor que serão exibidos. Neste caso, o eixo x terá como menor valor 1980 e como maior valor 2013, enquanto o eixo y terá como menor valor 0 e como maior valor 3000.
autorange=False: define se os limites do eixo serão ajustados automaticamente (True) ou não (False). Neste caso, os limites não serão ajustados automaticamente.
title='<b>Ano</b>': define o título do eixo. Neste caso, o eixo x terá o título "Ano", que é formatado em negrito (usando as tags HTML "" e "").
title='<b>Número de imigrantes</b>': define o título do eixo. Neste caso, o eixo y terá o título "Número de imigrantes", que é formatado em negrito (usando as tags HTML "<b>" e "</b>").
fig.update_layout(
    title=dict(
        text='<b>Imigração do Brasil para o Canadá no período de 1980 a 2013</b>',
        x=0.12,
        xanchor='left',
        font=dict(size=20)
    ),
    xaxis=dict(range=[1980, 2013], autorange=False, title='<b>Ano</b>'),
    yaxis=dict(range=[0, 3000], autorange=False, title='<b>Número de imigrantes</b>'),Copiar código
6 - É adicionado um botão "Play" para a animação usando o argumento updatemenus. Esse argumento é uma lista que define as opções de menu para a figura. O valor atribuído a essa lista é um dicionário, com as seguintes propriedades:

type='buttons': define que o menu será composto por botões.
showactive=False: define que nenhum botão estará ativo inicialmente.
buttons=[dict(label='Play', method='animate', args=[None, {'frame': {'duration': 100, 'redraw': True}, 'fromcurrent': True}])]: define o botão que será exibido no menu. Este botão tem a etiqueta "Play" (ou seja, "tocar"), que é exibida no próprio botão. O método animate é usado para ativar a animação dos dados. O argumento args é uma lista que contém dois elementos: o primeiro elemento é None, indicando que nenhum trace (ou camada) do gráfico será afetado pela animação, e o segundo elemento é um dicionário que especifica os parâmetros da animação. O parâmetro frame define a duração de cada quadro da animação e a atualização de cada quadro. O parâmetro fromcurrent define se o quadro atual deve ser mantido ou se a animação deve ser iniciada do primeiro quadro.
 updatemenus=[dict(
        type='buttons',
        showactive=False,
        buttons=[dict(
            label='Play',
            method='animate',
            args=[None, {'frame': {'duration': 100, 'redraw': True}, 'fromcurrent': True}]
        )]
    )],Copiar código
7- A largura e a altura do gráfico são definidas com os parâmetros width e height, respectivamente:

width=1000,
height=500 Copiar código
8 - Em seguida, as configurações de animação são definidas. A variável frames é uma lista de objetos Frame do Plotly, que contém as informações dos dados para cada quadro da animação. Cada quadro é representado por um objeto Frame que contém um único trace, que é um objeto Scatter. No caso deste código, cada Scatter representa um ponto no gráfico, onde X é o ano e Y é o número de imigrantes.

O loop for é usado para criar um objeto Frame para cada ano no conjunto de dados, até o último ano. O método iloc é usado para selecionar os valores do DataFrame dados_brasil a partir do índice 0 até o índice atual i+1, o que significa que cada quadro da animação adiciona um ponto adicional ao gráfico. A cada iteração, a lista frames é preenchida com um novo objeto Frame.

Por último, a lista frames é atribuída à propriedade frames do objeto Figure (fig) criado anteriormente. Isso permite que a animação seja exibida no gráfico quando o botão de controle de animação é pressionado. Cada frame contém os dados do gráfico para um determinado ano e é exibido em sequência quando o botão "Play" é clicado.

frames = [go.Frame(data=[go.Scatter(x=dados_brasil['ano'].iloc[:i+1], y=dados_brasil['imigrantes'].iloc[:i+1])]) for i in range(len(dados_brasil))]
fig.frames = framesCopiar código
9 - Por fim, a função fig.show() é chamada para exibir o gráfico animado no notebook. Quando o botão "Play" é pressionado, o gráfico será animado, mostrando a imigração do Brasil para o Canadá no período de 1980 a 2013.

Temos o código completo abaixo:

import plotly.graph_objs as go

# Criando uma figura
fig = go.Figure()

# Adicionando a linha do gráfico e definindo a espessura da linha
fig.add_trace(
    go.Scatter(x=[dados_brasil['ano'].iloc[0]], y=[dados_brasil['imigrantes'].iloc[0]], mode='lines', name='Imigrantes', line=dict(width=4))
)

# Definindo as configurações de layout
fig.update_layout(
    title=dict(
        text='<b>Imigração do Brasil para o Canadá no período de 1980 a 2013</b>',
        x=0.12,
        xanchor='left',
        font=dict(size=20)
    ),
    xaxis=dict(range=[1980, 2013], autorange=False, title='<b>Ano</b>'),
    yaxis=dict(range=[0, 3000], autorange=False, title='<b>Número de imigrantes</b>'),
    updatemenus=[dict(
        type='buttons',
        showactive=False,
        buttons=[dict(
            label='Play',
            method='animate',
            args=[None, {'frame': {'duration': 100, 'redraw': True}, 'fromcurrent': True}]
        )]
    )],
    width=1000, 
    height=500 
)

# Definir as configurações de animação
frames = [go.Frame(data=[go.Scatter(x=dados_brasil['ano'].iloc[:i+1], y=dados_brasil['imigrantes'].iloc[:i+1])]) for i in range(len(dados_brasil))]
fig.frames = frames

# Mostrando a figura
fig.show()Copiar código
Além disso, é importante destacar que as possibilidades de criação de animações são muito grandes. Podemos animar não só linhas, mas também pontos, barras, mapas e muito mais. A biblioteca Plotly oferece uma série de ferramentas e recursos para nos ajudar a criar visualizações incríveis e com alto grau de interatividade.