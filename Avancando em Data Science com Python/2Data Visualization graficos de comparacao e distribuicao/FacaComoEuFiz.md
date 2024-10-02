**Faça Como Eu Fiz** = **Mão na Massa**

## Aula 1: Preparando o Ambiente  
Neste curso, vamos construir um portfólio com as análises de duas bases de dados diferentes, explorando cada uma delas e respondendo aos questionamentos levantados em torno dessas duas bases de dados. Todas as bases estão no formato CSV e podem ser acessadas por meio do [Github do curso](https://github.com/alura-cursos/dataviz-graficos).

Bases de dados:

1 - Vendas de uma rede de lojas de departamentos que opera em todo Brasil;

2 - Distribuição de volumes e medidas de produtos de uma empresa de itens de limpeza:

a) Volume de um amaciante de 1L em um total de 1000 amostras medidas;
b) Medidas de altura, comprimento e largura de uma caixa de sabão em pó em um total de 1000 amostras medidas.
A cada aula, vamos passar por uma das bases de dados e planejar nossas análises de acordo com as perguntas que forem apresentadas, buscando respondê-las por meio da utilização de recursos visuais (gráficos e elementos visuais).

Antes de começar…
Para fazer este curso junto comigo você vai precisar baixar o notebook do curso e fazer o upload em seu Google Colab. Para que você consiga usar esse ambiente, é necessário ter uma conta Gmail, pois todo notebook ficará armazenado no Google Drive.

Agora com tudo pronto, vamos começar a pôr a mão na massa?

Bons estudos e vamos nessa!

## Faça como eu fiz: adicionando texto com destaques
No vídeo anterior orientamos a redução da área do gráfico para que possamos realizar uma etapa da visualização de dados nesta atividade.

O gráfico gerado neste vídeo pela função grafico_top_7() consegue responder ao questionamento levantado dentro do projeto: Qual é o top 7 produtos que mais apresentaram lucros em nosso catálogo durante o período representado?.

Entretanto, podemos adicionar algumas anotações a partir das observações do gráfico de barras gerado. Vamos observar o gráfico que foi produzido até o momento:

alt-text: Gráfico de barras criado com a biblioteca Seaborn e Matplotlib mostrando o top 7 produtos com maior lucro no catálogo das lojas de departamentos de 2016 a 2019. O eixo x foi retirado na construção do gráfico. Os valores do eixo y representam cada um dos produtos de cima para baixo: peças de reposição, pneus, ferramentas automotivas, pesticidas, ferramentas de jardinagem, ferramentas e vasos. Cada coluna possui os valores e tamanhos correspondentes ao lucro de cada produto. É possível notar 3 barras na cor azul, representando o departamento automotivo, 3 verdes, representando o departamento de jardinagem e paisagismo e 1 cinza, representando o departamento de materiais de construção

Note que temos uma série de interpretações que podemos realizar acerca dos dados apresentados, mas vamos focar em apresentar uma delas aqui.

Nesta atividade, vamos aprender a criar um único texto utilizando cores diferentes.

Atenção: O processo que será explicado na sequência está dentro do notebook do Colab, baixado ao longo do curso, na aba Adicionando texto com destaques logo após o gráfico de barras gerado no vídeo anterior.

Função para colorir texto
De maneira nativa, (com as funções e módulos padrões do Python e/ou das bibliotecas do Python) até o momento da gravação deste curso, ainda não existe uma forma de escrever texto colorido, a não ser que cada linha seja gerada separadamente com uma cor específica.

Para conseguir tal efeito, vamos adaptar uma função gerada por um usuário do [github no repositório](https://github.com/empathy87/storytelling-with-data) de visualizações de dados baseado no livro Storytelling com Dados, da Cole Nussbaumer Knaflic.

Para utilizá-la precisamos importar o sub-módulo transforms da biblioteca Matplotlib.

Vamos deixar o código completo deste processo na célula aqui abaixo. Aqui, não vamos explicar todo o funcionamento do código, mas basicamente vamos apontar alguns comportamentos.

from matplotlib import transforms

def texto_colorido(x, y, texto, cores, esp=20, ax=None, **kw):
    cores = list(reversed(cores))
    t = ax.transData
    canvas = ax.figure.canvas

    for i, linha in enumerate(reversed(texto.split('\n'))):
        frases = linha.split('||')
        for s, cor in zip(frases, cores[i]):
            texto = ax.text(x, y, s, color=cor, transform=t, **kw)
            texto.draw(canvas.get_renderer())
            ex = texto.get_window_extent()
            t = transforms.offset_copy(texto._transform, x=ex.width,
                                       units='dots')

        t = transforms.offset_copy(ax.transData, x=0, y=(i + 1) * esp, units='dots')
Copiar código
A função texto_colorido() é similar a função plt.text(). Ela basicamente recebe:

x e y: as coordenadas da escrita do texto
texto: o texto em formato de string
cores: as cores que vamos utilizar em cada linha numa lista de listas, onde cada item da lista de listas corresponde a cada linha
esp: o espaçamento entre linhas
ax: o eixo da figura onde desenhar o texto
(kw): propriedades da classe Texto que podem ser utilizadas na função
Outra coisa importante para entender são os delimitadores. Aqui esta função usa dois tipos de delimitadores:

|| : para definir a mudança de cores numa mesma linha. No código é definido como um separador de frases
\n : separador de linhas. Apenas a última linha não deve possuir o separador de linhas, pois ocasionaria em erro no código
Os outros métodos são para manipulação dos eixos e definição dos pontos de interesse para espaçamento das linhas e posição do texto.

Gerando o texto colorido no gráfico
Continuando, vamos gerar o texto colorido na lateral direita do gráfico. Primeiro, vamos chamar a função de geração do gráfico de barras e depois a função da geração do texto:

## Configurando o gráfico com parâmetros que potencializam a visualização dos dados

# Chamando a função do gráfico de barras
ax = grafico_top_7()

# Anotando uma conclusão no gráfico
texto_colorido(
    9.2e4, 3.25,                                                       			 # coordenadas
    'Os dados indicam que os 3 produtos que geram\n'                    # texto
    '$\\bf{maior\ lucro}$|| são do departamento ||$\\bf{Automotivo}$.\n'
    '\n'
    'Podemos notar também que o departamento de\n'
    '$\\bf{Jardinagem\ e\ paisagismo}$|| possui 3 produtos com\n'
    'uma boa margem de lucro, sendo que um deles está\n'
    'abaixo de ||$\\bf{50\ mil\ reais}$|| no período mencionado.',
    [[CINZA2],                       	           # linha 1                         		 # cores
     [CINZA1, CINZA2, AZUL2],         # linha 2
     [CINZA2],                                     # linha 3
     [CINZA2],                       	          # linha 4
     [VERDE1, CINZA2],                   # linha 5
     [CINZA2],                                    # linha 6
     [CINZA2, CINZA1, CINZA2]        # linha 7
    ],
    esp=22,				 # espaçamento
    ax=ax,				 # figura onde desenhar o texto
    fontsize=10)

fig = ax.get_figure()
Copiar código
Vamos observar as duas primeiras linhas do texto para explicar a funcionalidade da função:

…
    'Os dados indicam que os 3 produtos que geram\n'              		 # texto
    '$\\bf{maior\ lucro}$|| são do departamento ||$\\bf{Automotivo}$.\n'
...
    [[CINZA3],                       		 # linha 1                    			 # cores
     [CINZA1, CINZA3, AZUL2],           # linha 2
    ]
…
Copiar código
Note que na 1ª linha não existe o delimitador ( || ) o que demonstra que não houve uma divisão de frase, sendo a linha inteira de apenas uma cor [CINZA3].

Já na 2ª linha temos 2 delimitadores ( || ) que dividem o texto em três partes, ou seja, três cores diversas [CINZA1, CINZA3, AZUL2].

É possível utilizar também o recurso de colocar o texto em negrito nessa função por meio do mathtext $\\bf{texto}$. A barra invertida é para definir a separação das palavras com espaço.

Importante pontuar que é necessário passar quaisquer que sejam a quantidade de cores como uma lista dentro de uma lista de listas. Por exemplo, [ [CINZA3] , [CINZA1, CINZA3, AZUL2] ].

Agora, vamos rodar o nosso código com o fig = ax.get_figure() para resultar no seguinte gráfico:

alt-text: Gráfico de barras criado com a biblioteca Seaborn e Matplotlib mostrando o top 7 produtos com maior lucro no catálogo das lojas de departamentos de 2016 a 2019. O eixo x foi retirado na construção do gráfico. Os valores do eixo y representam cada um dos produtos de cima para baixo: peças de reposição, pneus, ferramentas automotivas, pesticidas, ferramentas de jardinagem, ferramentas e vasos. Cada coluna possui os valores e tamanhos correspondentes ao lucro de cada produto. É possível notar 3 barras na cor azul, representando o departamento automotivo, 3 verdes, representando o departamento de jardinagem e paisagismo e 1 cinza, representando o departamento de materiais de construção. Ao lado direito do gráfico possuímos o texto gerado na função texto_colorido()

O nosso gráfico está ainda mais bonito e informativo por meio dos insights que foram construídos na análise do gráfico.

## Desafio: gráficos de comparação - Colunas e barras
Vamos praticar a criação de gráficos de comparação (colunas e barras) que aprendemos até aqui. Para a prática, vamos seguir utilizando o conjunto de dados do relatório de vendas das lojas de departamentos de 2016 a 2019 que está disponível no [github do projeto](https://github.com/alura-cursos/dataviz-graficos/blob/master/dados/relatorio_vendas.csv).

Neste desafio, a missão é construir as visualizações que respondam aos questionamentos que compartilharemos aqui abaixo:

Desafio 1: Quais são os lucros das vendas por ano? Em qual ano obtivemos o maior lucro?

Desafio 2: Qual foi o faturamento (vendas) dos top 10 produtos durante o período de 2016 a 2019 do nosso conjunto de dados? Adicione um pequeno texto falando dos 3 produtos que mais venderam.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Para você criar e verificar seus códigos vamos deixar um notebook para resolução deste e dos próximos desafios. Você pode baixá-lo e fazer o upload do notebook no Google Colab ou criar o seu próprio.
### Opinião do instrutor  
Podem existir diversas formas de solucionar uma questão. Apresentamos abaixo uma sugestão de solução para cada problema, mas podem haver outras formas.

Desafio 1: Para o primeiro desafio vamos criar um gráfico de colunas com o valor dos lucros de 2016 a 2019 e destacar o ano com maior lucro.

Definindo a paleta de cores
AZUL1, AZUL2, AZUL3, AZUL4, AZUL5 = '#03045e', '#0077b6', "#00b4d8", '#90e0ef', '#CDDBF3'
CINZA1, CINZA2, CINZA3, CINZA4, CINZA5 = '#212529', '#495057', '#adb5bd', '#dee2e6', '#f8f9fa'
VERMELHO1, LARANJA1, AMARELO1, VERDE1, VERDE2 = '#e76f51', '#f4a261',	'#e9c46a', '#4c956c', '#2a9d8f'
Copiar código
Importando e tratando os dados
# Importando as bibliotecas
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Importando o relatório de vendas e atualizando a colunas de pedido para o tipo data
vendas = pd.read_csv("https://raw.githubusercontent.com/alura-cursos/dataviz-graficos/master/dados/relatorio_vendas.csv")
vendas["data_pedido"] = pd.to_datetime(vendas["data_pedido"], format="%Y-%m-%d")

# Criando um df com os dados desejados
df_lucro_ano = vendas.copy()
df_lucro_ano = df_lucro_ano[["data_pedido", "lucro"]]

# Gerando uma coluna que represente apenas os anos puxando-os da coluna data pedido
df_lucro_ano["ano"] = df_lucro_ano.data_pedido.dt.year
df_lucro_ano.drop(labels = "data_pedido", axis = 1, inplace=True)

# Agrupando os dados por ano
df_lucro_ano = df_lucro_ano.groupby(["ano"]).aggregate("sum")

df_lucro_ano
Copiar código
Gerando o gráfico
# Área do gráfico e tema da visualização
fig, ax = plt.subplots(figsize=(10,4))
sns.set_theme(style="white")

# Definindo as cores do gráfico
cores = []
for ano in df_lucro_ano.index:
  if df_lucro_ano.loc[ano,"lucro"] == df_lucro_ano["lucro"].max():
    cores.append(AZUL2)
  else:
    cores.append(AZUL5)

# Gerando o gráfico de colunas
ax = sns.barplot(data = df_lucro_ano, x = df_lucro_ano.index, y="lucro", palette = cores)

# Personalizando o gráfico
ax.set_title("Lucro das vendas das lojas de departamentos de\n2016 a 2019", loc="left", fontsize = 18, color = CINZA1)
ax.set_xlabel("")
ax.set_ylabel("")
ax.xaxis.set_tick_params(labelsize = 14, labelcolor= CINZA2)
sns.despine(left= True, bottom = True)

# Escrevendo os valores de cada barra no gráfico
ax.set_yticklabels([])
for i, valor in enumerate(df_lucro_ano["lucro"]):
  qtd = f'R$ {valor:,.0f}'.replace(",",".")
  offset = 1e4
  ax.text(i, valor + offset, qtd, color = CINZA2, fontsize = 12, ha = "center", va = "center")

# Anotando uma conclusão no gráfico
ax.text(3.5, 1e5,
         'O maior lucro registrado foi no ano $\\bf{2019}$.\n'
         'Em comparação com 2018, o lucro\n'
         'subiu aproximadamente $\\bf{14,04}$%.',
         fontsize=14, linespacing=1.45, color=AZUL2)

# Exibindo o gráfico
plt.show()
Copiar código
Saída:

alt-text: Gráfico de colunas criado com a biblioteca Seaborn e Matplotlib mostrando os lucros das vendas das lojas de departamentos de 2016 a 2019. É possível notar no eixo x cada ano do intervalo de tempo já mencionado. O eixo y foi retirado do gráfico por meio do código. As 3 primeiras colunas possuem uma cor azul clara e a última um tom de azul mais escuro. Cada coluna tem o tamanho correspondente ao lucro do ano e em cima dela o valor do lucro em reais. à direita da última coluna existe um texto gerado pela função ax.text()

Desafio 2: Para o segundo desafio vamos criar um gráfico de barras de vendas por departamento no período de 2016 a 2019 em ordem decrescente e adicionar um texto falando dos 3 departamentos que mais lucraram.

Importando e tratando os dados
# Importando as bibliotecas
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Importando o relatório de vendas e atualizando a colunas de pedido para o tipo data
vendas = pd.read_csv("https://raw.githubusercontent.com/alura-cursos/dataviz-graficos/master/dados/relatorio_vendas.csv")
vendas["data_pedido"] = pd.to_datetime(vendas["data_pedido"], format="%Y-%m-%d")

# Criando um df com os dados desejados
fat_produto = vendas.copy()
fat_produto = fat_produto[["tipo_produto", "vendas"]]

# Agrupando os dados por tipo_produto, ordenando de maneira decrescente pelas vendas e selecionando os 10 primeiros
fat_produto = fat_produto.groupby(["tipo_produto"]).agg("sum").sort_values("vendas", ascending = False)
top_10 = fat_produto[:10]
top_10
Copiar código
Código para gerar o texto colorido
# Código para gerar o texto colorido

from matplotlib import transforms

def texto_colorido(x, y, texto, cores, esp=20, ax=None, **kw):
    cores = list(reversed(cores))
    t = ax.transData
    canvas = ax.figure.canvas

    for i, linha in enumerate(reversed(texto.split('\n'))):
        frases = linha.split('||')
        for s, cor in zip(frases, cores[i]):
            texto = ax.text(x, y, s, color=cor, transform=t, **kw)
            texto.draw(canvas.get_renderer())
            ex = texto.get_window_extent()
            t = transforms.offset_copy(texto._transform, x=ex.width, 
                                       units='dots')

        t = transforms.offset_copy(ax.transData, x=0, y=(i + 1) * esp, units='dots')
Copiar código
Gerando o gráfico
# Área do gráfico e tema da visualização
fig, ax = plt.subplots(figsize=(10,4))
fig.subplots_adjust(right=0.7)
sns.set_theme(style="white")

# Definindo as cores do gráfico: 3 primeiro em azul e restante em cinza 
cores = [AZUL2 if i < 3 else CINZA3 for i in range(10)]

# Gerando o gráfico de barras 
ax = sns.barplot(data = top_10, x="vendas", y = top_10.index, palette = cores)

# Personalizando o gráfico
ax.set_title('Top 10 produtos com maiores vendas no catálogo (2016-2019)\n', fontsize=18, color=CINZA1, loc='left')
ax.set_xlabel('')
ax.set_ylabel('')
ax.set_xticklabels([])
ax.yaxis.set_tick_params(labelsize=10, labelcolor = CINZA2)
sns.despine(left = True, bottom = True)

# Escrevendo os valores de cada barra no gráfico
for i, valor in enumerate(top_10['vendas']):
    qtd = f'R$ {valor:,.0f}'.replace(',','.')  
    offset = 1e4  # offset de 10.000
    ax.text(valor - offset, i, qtd, color= CINZA5, fontsize=10, fontweight='bold', ha='right', va='center')

# Gerando o texto colorido
texto_colorido(
    1.05e6, 4,                                                      # coordenadas
    'Os dados indicam que os 3 produtos que || $\\bf{mais}$\n'     # texto
    'venderam foram: || $\\bf{pneus,\ ferramentas\ e\ vasos}$.\n'
    '\n'
    'Podemos notar no período mencionado também que as\n'
    'ferramentas de jardinagem e materiais de revestimento\n' 
    'também possuem uma boa saída.',
    [[CINZA2, CINZA1],                # linha 1                     # cores
     [CINZA2, AZUL2],                 # linha 2
     [CINZA2],                        # linha 3
     [CINZA2],                        # linha 4
     [CINZA2],                        # linha 6
     [CINZA2]
    ],
    esp=22,         # espaçamento
    ax=ax,          # figura onde desenhar o texto
    fontsize=10)

# Exibindo o gráfico
plt.show()
Copiar código
Saída:

alt-text: Gráfico de barras criado com a biblioteca Seaborn e Matplotlib mostrando o top 10 produtos com maiores vendas no catálogo das lojas de departamentos de 2016 a 2019. O eixo x foi retirado na construção do gráfico. Os valores do eixo y representam cada um dos produtos de cima para baixo: pneus, ferramentas, vasos, ferramentas de jardinagem, materiais de revestimento, equipamentos de limpeza, ferramentas automotivas, peças de reposição, encanamentos e mobiliário exterior. Cada coluna possui os valores e tamanhos correspondentes às vendas de cada produto. É possível notar 3 barras na cor azul, representando os três produtos mais vendidos e o restante cinza, representando os outros produtos que mais venderam

A prática é sempre muito importante para fixar o conteúdo, ainda mais de um assunto tão importante que é o de visualização de dados. A análise de dados por meio de recursos visuais facilita a interpretação das pessoas sobre os dados e apresenta de maneira simples e direta o que eles representam e quais insights podemos adquirir nessa forma de exploração dos dados.

Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é extremamente importante para o seu crescimento dentro da carreira de dados. Portanto, busque realizar os exercícios propostos e veja como isso pode te ajudar a progredir em suas habilidades em visualização de dados.

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.

## Aula 2
### Desafio: gráficos de comparação - Colunas e barras empilhadas
Vamos praticar a criação de gráficos de comparação representando os valores agrupados por colunas e/ou barras. Para esse desafio, vamos seguir utilizando o conjunto de dados do relatório de vendas das lojas de departamentos de 2016 a 2019 que está disponível no github do projeto.

Neste desafio, a missão é construir as visualizações que respondam aos questionamentos abaixo:

Desafio 1: Como estão divididas as vendas das lojas de departamentos na Região Centro-Oeste nos anos de 2017 e 2018? O mesmo estado permaneceu como o que mais vendeu nesta região?

Desafio 2: Analisando cada departamento, como estão divididos os modos de envio em cada um deles percentualmente?

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Caso ainda não tenha baixado o notebook dos desafios aproveite para baixá-lo agora. Ele possui as células e textos para você construir suas soluções e pode te ajudar a verificar seus códigos. Você pode baixá-lo para resolver as atividades e desafios testando os seus conhecimentos até o momento.  
### Opinião do instrutor

Podem existir diversas formas de solucionar uma questão. Apresentamos abaixo uma sugestão de solução para cada problema, mas podem haver outras formas.

Desafio 1: Para o primeiro desafio vamos criar um gráfico de colunas empilhadas com o valor das vendas de 2017 e 2018 dos estados da Região Centro-Oeste do Brasil, destacando os estados com maior venda em cada ano.

Importando e tratando os dados
# Importando as bibliotecas
import pandas as pd

# Importando o relatório de vendas e atualizando a colunas de pedido para o tipo data
vendas = pd.read_csv("https://raw.githubusercontent.com/alura-cursos/dataviz-graficos/master/dados/relatorio_vendas.csv")
vendas["data_pedido"] = pd.to_datetime(vendas["data_pedido"], format="%Y-%m-%d")

# Criando um df com os dados desejados
vendas_co = vendas.copy()
vendas_co = vendas_co[['data_pedido','regiao', 'estado', 'vendas']]

# Gerando uma coluna que represente apenas os anos puxando-os da coluna data pedido
vendas_co['ano'] = vendas_co.data_pedido.dt.year

# Selecionando apenas os dados do Centro-Oeste dos anos de 2017 e 2018 e removendo as colunas de data_pedido e região
vendas_co = vendas_co.query("regiao == 'Centro-Oeste' and (ano == 2017 or ano == 2018)")
vendas_co.drop(labels = ["data_pedido","regiao"], axis = 1, inplace = True)

vendas_co
Copiar código
Gerando a tabela cruzada
# Criando uma tabela cruzada (crosstab) com os valores de venda de cada ano por estado
vendas_co_ano = pd.crosstab(index = vendas_co.ano, columns = vendas_co.estado, 
                         values = vendas_co.vendas, aggfunc = "sum")

vendas_co_ano
Copiar código
Gerando o gráfico
# Definindo as cores do gráfico
cores = [VERMELHO1, AMARELO1, VERDE1, AZUL2]

# Gerando o gráfico de colunas empilhadas 
ax = vendas_co_ano.plot(kind="bar", stacked=True, figsize=(8,8), color = cores)

# Personalizando o gráfico
ax.set_title('Vendas das lojas de departamentos na Região Centro-Oeste\nentre os anos de 2017 a 2018', 
             loc='left', fontsize=16, color = CINZA1)
ax.set_xlabel('')
ax.set_ylabel('')
ax.set_yticklabels([])
ax.xaxis.set_tick_params(labelsize=14, labelcolor = CINZA2, rotation = 0)
ax.set_frame_on(False)

# remover todos os ticks do eixo x e y
ax.tick_params(axis="both", which ="both", length=0)

# Anotando uma conclusão no gráfico
ax.text(-0.8, 1e5, 'O estado de Goiás\nrealizou mais vendas\nnas unidades do\nCentro-Oeste em 2017.',
        fontsize=10, linespacing=1.2, color=AZUL1)
ax.text(1.3, 8e4, 'O Distrito Federal passou\no estado de Goiás em vendas\nno ano de 2018.',
        fontsize=10, linespacing=1.2, color=AZUL1)

# Personalizando a legenda
ax.legend(bbox_to_anchor=(1,1), reverse = True, title= "Estado", title_fontsize = 10, fontsize = 10)

# Adicionando os valores 
for container in ax.containers:
  labels = [f'R$ {valor.get_height()/1000:,.2f} mil'.replace(",",".") for valor in container]
  ax.bar_label(container, label_type="center", labels = labels, size = 10, color = CINZA5, fontweight = "bold")

fig = ax.get_figure()
Copiar código
Saída:

alt-text: Gráfico de colunas empilhadas criado com a biblioteca Pandas mostrando as vendas das lojas de departamentos na Região Centro-Oeste entre os anos de 2017 e 2018. É possível notar no eixo x os dois anos mencionados. O eixo y foi retirado por código. Cada coluna possui 4 barras de cores diferentes: a laranja simboliza o Distrito Federal, a amarela ouro simboliza o estado de Goiás, a verde o estado de Mato Grosso e, por fim, a azul-escuro simboliza o estado de Mato Grosso do Sul. Cada barra tem o tamanho correspondente a de vendas do estado que representa com os valores centralizados em cada uma delas. No lado esquerdo da 1ª coluna e no lado direito da 2ª coluna temos os textos gerados pela função ax.text()

Desafio 2: Para o segundo desafio, vamos criar um gráfico de barras empilhadas com valores relativos aos modos de envio para cada departamento das lojas de departamentos no período de 2016 a 2019.

Importando e tratando os dados
# Importando as bibliotecas
import pandas as pd

# Importando o relatório de vendas
vendas = pd.read_csv("https://raw.githubusercontent.com/alura-cursos/dataviz-graficos/master/dados/relatorio_vendas.csv")

# Criando um df com os dados desejados
df_depart = vendas.copy()
df_depart = df_depart[['departamento','modo_envio']]

## Criando uma tabela cruzada (crosstab) com a frequência de modos de envio por departamento
df_depart = pd.crosstab(index = df_depart.departamento, columns = df_depart.modo_envio, normalize = "index")

df_depart
Copiar código
Código para gerar o texto colorido
# Código para gerar o texto colorido

from matplotlib import transforms

def texto_colorido(x, y, texto, cores, esp=20, ax=None, **kw):
    cores = list(reversed(cores))
    t = ax.transData
    canvas = ax.figure.canvas

    for i, linha in enumerate(reversed(texto.split('\n'))):
        frases = linha.split('||')
        for s, cor in zip(frases, cores[i]):
            texto = ax.text(x, y, s, color=cor, transform=t, **kw)
            texto.draw(canvas.get_renderer())
            ex = texto.get_window_extent()
            t = transforms.offset_copy(texto._transform, x=ex.width, 
                                       units='dots')

        t = transforms.offset_copy(ax.transData, x=0, y=(i + 1) * esp, units='dots')
Copiar código
Gerando o gráfico
# Definindo as cores do gráfico
cores = [AZUL1, AZUL2, AZUL3, AZUL4]

# Gerando o gráfico de barras empilhadas 
ax = df_depart.plot(kind="barh", stacked=True, figsize=(12,6), color = cores, legend = None)
ax.set_title("Distribuição percentual dos modos de envio por cada departamento (2016-2019)\n", 
             fontsize=16, loc="left", color=CINZA1)
ax.set_xlabel('')
ax.set_ylabel('')
ax.set_xticklabels([])
ax.yaxis.set_tick_params(labelsize=12, color = CINZA2)
ax.set_frame_on(False)

# remover todos os ticks do eixo x e y
ax.tick_params(axis='both', which='both', length=0)

# legenda dos dados
texto_colorido(0, 2.3, '$\\bf{24 horas}$ | || $\\bf{Econômica}$  | || $\\bf{Entrega\ padrão}$ | || $\\bf{Envio\ rápido}$', cores = [cores], ax=ax, fontsize=12)

# Valores das barras
for container in ax.containers:
    labels = [f'{valor.get_width()*100:.1f}%' for valor in container]
    ax.bar_label(container, label_type='center', labels = labels, size = 12, color = CINZA5, fontweight='bold')

fig = ax.get_figure()
Copiar código
Saída:

alt-text: Gráfico de barras empilhadas criado com a biblioteca Pandas mostrando a distribuição percentual dos modos de envio por cada departamento de 2016 a 2019. O eixo x foi retirado por código. O eixo Y possui o nome de três departamentos: materiais de construção, jardinagem, paisagismo e automotivo. Cada barra possui 4 barras menores de 4 tons de azul diferentes: a mais escura simboliza o modo de envio de 24 horas, a escura o modo de envio econômico, a clara o modo de entrega padrão e, por fim, a mais clara o modo de envio rápido. Cada barra menor tem o tamanho correspondente a porcentagem da quantidade de envios realizados naquele departamento com os valores centralizados em cada uma delas.

A prática é sempre muito importante para fixar o conteúdo, ainda mais de um assunto tão importante que é o de visualização de dados. A análise de dados por meio de recursos visuais facilita a interpretação das pessoas sobre os dados e apresenta de maneira simples e direta o que eles representam e quais insights podemos adquirir nessa forma de exploração dos dados.

Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é extremamente importante para o seu crescimento dentro da carreira de dados. Portanto, busque realizar os exercícios propostos e veja como isso pode te ajudar a progredir em suas habilidades em visualização de dados

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.

## Aula 03
### Desafio: gráficos de comparação - Séries de tempo
Vamos praticar a criação de gráficos de séries de tempo. Para a prática, vamos seguir utilizando o conjunto de dados do relatório de vendas das lojas de departamentos de 2016 a 2019 que está disponível no github do projeto.

Neste desafio, a missão é construir as visualizações que respondam aos questionamentos que compartilharemos aqui abaixo:

Desafio 1: Como estão as vendas por semestre no estado em que você mora ou que deseja conhecer? Destaque os valores máximos e mínimos de venda para apresentá-los ao seu público.

Dica: Para agrupar os dados por semestre você pode utilizar a função resample da seguinte forma: resample(“2Q”, closed = “left”)

Desafio 2: Compare os lucros anuais dos estados da região Nordeste por meio de um gráfico de linhas.

Sugestão: No Desafio 2, utilize o Plotly para possibilitar ao usuário a escolha entre linhas que deseja visualizar.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Caso ainda não tenha baixado o notebook dos desafios aproveite para baixá-lo agora. Ele possui as células e textos para você construir suas soluções e pode te ajudar a verificar seus códigos. Você pode baixar ele para resolver as atividades e desafios testando os seus conhecimentos até o momento.


### Opinião do instrutor

Podem existir diversas formas de solucionar uma questão. Apresentamos abaixo uma sugestão de solução para cada problema, mas podem haver outras formas.

Desafio 1: Para o primeiro desafio vamos criar um gráfico de linha com o valor das vendas, por exemplo, do estado da Bahia, destacando os valores máximos e mínimos das vendas no período.

Importando e tratando os dados
# Importando as bibliotecas
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.dates as mdates

# Importando o relatório de vendas e atualizando a colunas de pedido para o tipo data
vendas = pd.read_csv("https://raw.githubusercontent.com/alura-cursos/dataviz-graficos/master/dados/relatorio_vendas.csv")
vendas["data_pedido"] = pd.to_datetime(vendas["data_pedido"], format="%Y-%m-%d")

# Criando um df com os dados desejados
df_estado = vendas.copy()
df_estado = df_estado.query('estado == "Bahia"')[["data_pedido", "vendas"]]

# Agrupando as vendas por final do semestre (2Q)
df_estado.set_index("data_pedido", inplace = True)
df_estado = df_estado.resample("2Q", closed="left").agg("sum")
df_estado = df_estado.reset_index()
df_estado.head()
Copiar código
Gerando o gráfico
# Área do gráfico e tema da visualização
fig, ax = plt.subplots(figsize=(16,4))

# Resgatando o valor minimo, maximo das vendas
venda_min = df_estado.vendas.min()
venda_max = df_estado.vendas.max()
valores = df_estado.vendas.values

# Gerando a lista com os pontos a marcar (True apenas para mínimo e máximo)
pontos_a_marcar = list((valores == venda_min) | (valores == venda_max))

# Criando o gráfico de linha das vendas 
ax.plot(df_estado["data_pedido"], df_estado["vendas"], lw = 3, color = AZUL5, marker = "o",
          markersize = 10, markerfacecolor = AZUL2, markevery =  pontos_a_marcar)

## Personalizando o gráfico
ax.set_title('Vendas no estado da Bahia (2016-2019)', fontsize = 16, loc='left', pad = 20)
ax.set_xlabel('Meses', fontsize = 14)
ax.set_ylabel('')
ax.grid(axis = "y", linestyle="--")
ax.set_frame_on(False)

# remover todos os ticks do eixo x e y
ax.tick_params(axis='both', which='both', length=0)

# Descrevendo o limite mínimo e máximo do eixo y
plt.ylim(0, 1.25e5)

# Definindo o intervalo semestral para os dados
ax.xaxis.set_major_locator(mdates.MonthLocator(bymonth = [6,12]))
labels = ["1º Sem, 2016", "2º Sem, 2016", "1º Sem, 2017", "2º Sem, 2017", 
          "1º Sem, 2018", "2º Sem, 2018", "1º Sem, 2019", "2º Sem, 2019"]
ax.set_xticks(ax.get_xticks())
ax.set_xticklabels(labels, ha = "left")

# Escrevendo texto nos pontos de destaque
for x, y in zip(df_estado.data_pedido, df_estado.vendas):
  if y == venda_min:
    ax.text(x, y = y - 1.2e4, s = f" O 1º Semestre de 2017 registrou \n a única venda abaixo de R$ 40 mil", fontsize = 10)
  if y == venda_max:
    ax.text(x, y = y - 1.2e4, s = f" As vendas ultrapassaram pela \n 1ª vez a faixa de R$ 100 mil \n no 2º Semestre de 2019", fontsize = 10)

plt.show()
Copiar código
Saída:

alt-text: Gráfico de linha criado com a biblioteca Matplotlib mostrando as vendas das lojas de departamentos no estado da Bahia de 2016 a 2019. É possível notar no eixo x 8 rótulos representando os semestres do período. O eixo y possui valores de 0 até 120.000. A linha em um tom de azul mais claro representa as vendas em cada semestre, com apenas 2 marcadores apontando os valores mínimos e máximos no período. Cada um possui um texto explicando os dados que foram gerados pelo ax.text()

Desafio 2: Para o segundo desafio vamos selecionar os dados da região Nordeste, gerando uma tabela cruzada com os valores dos lucros de cada estado desta região. Em seguida, vamos gerar um gráfico de linhas com esses dados.

Importando e tratando os dados
# Importando as bibliotecas
import pandas as pd
import plotly.express as px

# Importando o relatório de vendas e atualizando a colunas de pedido para o tipo data
vendas = pd.read_csv("https://raw.githubusercontent.com/alura-cursos/dataviz-graficos/master/dados/relatorio_vendas.csv")
vendas["data_pedido"] = pd.to_datetime(vendas["data_pedido"], format="%Y-%m-%d")

# Criando um df com os dados desejados
df_ne = vendas.copy()
df_ne = df_ne.query("regiao == 'Nordeste'")[["estado","data_pedido", "lucro"]]
Copiar código
Gerando a tabela cruzada
# Criando uma tabela cruzada (crosstab) com os valores de lucro por dia por estado
df_estados_ne = pd.crosstab(index = df_ne.data_pedido, columns = df_ne.estado, values = df_ne.lucro, aggfunc="sum")

# Agrupando os lucros por ano
df_estados_ne = df_estados_ne.resample('Y').agg('sum')
df_estados_ne = round(df_estados_ne/1e3, 2)
df_estados_ne
Copiar código
Gerando o gráfico
# Importando a biblioteca
import plotly.express as px

# Gerando um gráfico de linha com os lurcos das lojas por ano dividido por estado da região nordeste
fig = px.line(df_estados_ne, x=df_estados_ne.index, y=df_estados_ne.columns, markers = True, labels={"estado": "Estados"},
              color_discrete_sequence=[AZUL2, VERMELHO1, AMARELO1 , VERDE1, CINZA3, AZUL5, LARANJA1, CINZA1, AZUL4])

# Ajustando o layout do gráfico
fig.update_layout(width=1300, height=600, font_family = 'DejaVu Sans', font_size=15,
                  font_color= CINZA2, title_font_color= CINZA1, title_font_size=24,
                  title_text='Lucros das lojas de departamentos por ano na Região Nordeste' +
                             '<br><sup size=1 style="color:#555655">De 2016 a 2019</sup>',
                  xaxis_title='', yaxis_title='', plot_bgcolor= CINZA5)

# Ajustando os ticks do eixo y para o formato em milhar
fig.update_yaxes(tickprefix="R$ ", ticksuffix=" mil")

# Ajustando o eixo x com os labels dos anos
labels = ['2016', '2017', '2018', '2019']
fig.update_xaxes(ticktext = labels, tickvals=df_estados_ne.index)

# Dados ao passar o mouse (hover)
fig.update_traces(mode="markers+lines", hovertemplate = "<b>Período:</b> %{x} <br> <b>Lucro:</b> %{y}")

fig.show()
Copiar código
Saída:

alt-text: Gráfico de linhas criado com a biblioteca Plotly com os lucros das lojas de departamentos por ano na Região Nordeste do Brasil de 2016 a 2019. É possível notar no eixo x 4 rótulos representando cada ano do período. O eixo y possui valores de 0 até 30.000 reais. Cada linha representa as vendas anuais dos 9 estados da região com os marcadores apontando o valor de cada ano. São ao todo 9 linhas com nove cores diversas

A prática é sempre muito importante para fixar o conteúdo, ainda mais de um assunto tão importante que é o de visualização de dados. A análise de dados por meio de recursos visuais facilita a interpretação das pessoas sobre os dados e apresenta de maneira simples e direta o que eles representam e quais insights podemos adquirir nessa forma de exploração dos dados.

Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é extremamente importante para o seu crescimento dentro da carreira de dados. Portanto, busque realizar os exercícios propostos e veja como isso pode te ajudar a progredir em suas habilidades em visualização de dados

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.


## Aula 4
### Faça como eu fiz: elementos de um boxplot
Aprendemos no vídeo anterior a identificar visualmente os elementos de um boxplot e como ele pode ser utilizado para representar a distribuição dos dados em nosso dataset. Agora, para fixarmos o conteúdo e nos preparar para o 2º desafio na próxima atividade auxiliar, vamos diferenciar esses elementos examinando a sua importância dentro da visualização

Os elementos principais de um boxplot são:

Quartis: dividem os dados ordenados em quatro partes iguais. O primeiro quartil (Q1) representa o valor abaixo do qual está 25% dos dados, o segundo quartil (Q2) representa a mediana, ou seja, o valor que divide os dados em duas partes iguais (50%), e o terceiro quartil (Q3) representa o valor abaixo do qual está 75% dos dados.

Intervalo interquartil: representado no desenho do boxplot como a caixa, o intervalo interquartil é a subtração entre o valor do terceiro quartil (Q3) pelo primeiro quartil (Q1). Ele representa a amplitude dos dados centrais, onde fica concentrada a metade dos valores. Para calculá-lo por meio da linguagem Python a partir de uma coluna de dados podemos escrever o código da seguinte forma:

IIQ = dados["nome_coluna"].quantile(0.75) - dados["nome_coluna"].quantile(0.25)
IIQ 
Copiar código
Limites máximo e mínimo: definem a faixa dos valores considerados “normais” ou “não-discrepantes”. São basicamente utilizados para identificar outliers. Geralmente, adota-se uma boa prática de determinar os limites por meio da soma, no caso do limite superior, ou subtração, no caso do limite inferior, do produto de 1,5 pelo intervalo interquartil (IIQ). Os valores fora desses dois limites são considerados outliers. Para calculá-lo por meio da linguagem Python a partir de uma coluna de dados podemos escrever o código da seguinte forma:
limite_superior = dados["nome_coluna"].quantile(0.75) + 1.5 * IIQ
limite_inferior = dados["nome_coluna"].quantile(0.25) - 1.5 * IIQ
print(f"Limite superior = {limite_superior}", f"\nLimite inferior = {limite_inferior}")
Copiar código
Outliers: são os valores que estão além dos limites máximos e mínimos mencionados acima. Esses valores são representados individualmente no gráfico do boxplot, geralmente como pontos ou asteriscos. Outliers podem indicar valores extremos ou erros de medição.
Agora que sabemos mais sobre o boxplot, que apresenta em uma só visualização várias medidas de distribuição dos dados: os quartis, a mediana, o intervalo interquartil e a presença de outliers, vamos partir para a resolução de mais um desafio na próxima atividade.
### Opinião do instrutor
Se você compreendeu os elementos do boxplot, suas utilidades e fórmulas para calcular essa métricas, estará pronto(a) para resolver os desafios desta aula. Tente testar o que aprendeu até aqui com algum tipo de dataset que desejar ou até mesmo ir além nos gráficos dos Desafios no final desta aula.

Experimente pesquisar na documentação do pandas e do seaborn sobre as funções e métodos utilizados até aqui para entender mais a fundo sobre a distribuição de dados em Python.  

### Desafio: gráficos de distribuição de dados  
Vamos praticar a criação de gráficos de distribuição de dados. Para esse desafio, vamos trabalhar com duas base de dados diferentes: a primeira será um dataset com as idades de uma amostra da população do município de Cidade Alegre, cidade fictícia que utilizamos em uma de nossas atividades, e a segunda será o dataset dos volumes do amaciante que utilizamos durante essa aula, que está disponível no github do projeto.

Neste desafio, a missão é construir as visualizações que respondam aos questionamentos que compartilharemos aqui abaixo:

Desafio 1: Baixe a base de dados com as amostras das idades dos moradores do município de Cidade Alegre e crie os histogramas de colunas e de linha lado a lado, buscando interpretar as diferenças entre eles e o que podem representar separadamente. Adicione também uma linha que define a mediana da distribuição no histograma de linha e escreva o valor dessa medida no gráfico.

Dica 1: Para desenhar os gráficos separados, utilize a mesma ideia que executamos no gráfico de barras empilhadas: fig, axs = plt.subplots(n_linhas, n_colunas, figsize=(largura, altura)).

Dica 2: E, para desenhar 2 ou mais gráficos no seaborn, precisamos passar um parâmetro ax para a função de desenho do visual, por exemplo, sns.barplot(ax = axs[0], …)

Desafio 2: Represente no boxplot dos volumes do amaciante os limites superiores e inferiores do diagrama de caixa. Comente sobre o resultado encontrado ao desenhar esses limites no boxplot.

Dica: Para conseguir definir os limites superiores e inferiores, calcule o intervalo interquartil dos dados e, logo em seguida, cada um dos limites, seguindo as fórmulas do Faça como eu fiz: elementos de um boxplot.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Caso ainda não tenha baixado o notebook dos desafios aproveite para baixá-lo agora. Ele possui as células e textos para você construir suas soluções e pode te ajudar a verificar seus códigos. Você pode baixar ele para resolver as atividades e desafios testando os seus conhecimentos até o momento.

### Opinião do Instrutor
Podem existir diversas formas de solucionar uma questão. Apresentamos abaixo uma sugestão de solução para cada problema, mas podem haver outras formas.

Desafio 1: Para o primeiro desafio vamos criar os histogramas de colunas e de linha e adicionar uma linha que representa a mediana da distribuição no histograma de linha.

Importando os dados
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

dados = pd.read_csv("pop_idade.csv")
dados.head()
Copiar código
Gerando o gráfico
# Área do gráfico e tema da visualização
fig, axs = plt.subplots(1, 2, figsize=(15,6))
sns.set_theme(style="white")

# Título dos gráficos
fig.suptitle("Distribuição da idade da população de Cidade Alegre \npara uma amostra de 500 pessoas", 
             fontsize=18, color=CINZA1, x = 0.1, y = 1.05, ha="left")

# GRÁFICO 1 - Histograma de Colunas

sns.histplot(ax = axs[0], data = dados, x = "idade", binwidth = 5, color = AZUL2)
axs[0].set_title('Distribuição para um intervalo de 5 anos', size=14, color=CINZA1, x = 0.35,  pad = 10)
axs[0].set_xlabel('Idade', fontsize = 14)
axs[0].set_ylabel('Quantidade', fontsize = 14)
axs[0].yaxis.set_tick_params(labelsize=12, labelcolor = CINZA2)
axs[0].xaxis.set_tick_params(labelsize=12, labelcolor = CINZA2)
sns.despine()

# GRÁFICO 2 - Histograma de Linhas

sns.kdeplot(ax = axs[1], data = dados, x = "idade", color = AZUL2)
axs[1].set_title('Com as medidas de tendência central', size=14, color=CINZA1, x = 0.35,  pad = 10)
axs[1].set_xlabel('Idade', fontsize = 14)
axs[1].set_ylabel('')
axs[1].yaxis.set_tick_params(labelsize=12, labelcolor = CINZA2)
axs[1].set_yticklabels([])
sns.despine()

# gerando a linha que define a mediana e anotando seu valor
axs[1].vlines(x = dados.idade.median(), ymin = 0, ymax = 0.04, colors = CINZA3, linestyles = "--")
axs[1].text(0.6, 0.6, f'Mediana = {int(dados.idade.median())} anos', fontsize=14, color = CINZA3, transform=axs[1].transAxes)

plt.show()
Copiar código
Saída:

alt-text: Figura com duas visualizações: Histograma de colunas e Histograma de linha, ambas criadas com a biblioteca Seaborn e Matplotlib e mostrando a distribuição da idade da população de Cidade Alegre para uma amostra de 500 pessoas. À esquerda temos um histograma de colunas onde é possível notar no eixo x os intervalos de idade de 10 em 10 anos, partindo de 0 até 80 anos. Os valores do eixo y variam de 0 a 100. Cada coluna do histograma possui o tamanho correspondente a quantidade de pessoas com certa faixa de idade. Todas as colunas estão na cor azul. Já, no gráfico à direita, temos um histograma de linha onde é possível notar no eixo x os intervalos de idade de 20 em 20 anos, partindo de 0 até 80 anos. Os rótulos do eixo foram retirados por código. É representada uma linha azul em forma de sino da distribuição normal da idade da população com uma mediana de 35 anos, representada por uma linha cinza cortando verticalmente o gráfico em duas partes. A curva representa a distribuição das pessoas nas faixas de idade

Desafio 2: Para o segundo desafio vamos construir o boxplot que montamos na aula, ajustando algumas etapas. Vamos apenas representar os intervalos máximos e mínimos na visualização, primeiro calculando o intervalo interquartil (IIQ) e utilizando esse valor na definição dos valores máximos e mínimos dentro dos parâmetros “normais” de um boxplot.

Importando e tratando os dados
# Importando as bibliotecas
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.patches import Ellipse
import seaborn as sns

# Importando a base de dados dos volumes de um amaciante em 1000 amostras realizadas
vol_amaciante = pd.read_csv("https://raw.githubusercontent.com/afonsosr2/dataviz-graficos/master/dados/volume_amaciante.csv")
Copiar código
Gerando o gráfico
# Área do gráfico e tema da visualização
fig, ax = plt.subplots(figsize=(6,8))
sns.set_theme(style="white")

# Gerando o boxplot
ax = sns.boxplot(data = vol_amaciante, y = "Volume", orient = "v", color = AZUL2)

## Personalizando o gráfico
plt.suptitle('Boxplot do volume do amaciante', size=18, color=CINZA1, ha = 'right', x = 0.81, y = 0.97)
plt.title('para uma amostra de 1000 unidades', fontsize=14, color=CINZA2, pad = 15, loc = "left")
ax.set_xlabel('')
ax.set_ylabel('Volume (ml)', fontsize = 14)
ax.yaxis.set_tick_params(labelsize=12, labelcolor = CINZA2)
sns.despine(bottom=True)

# Calculando o intervalo interquartil(IIQ) e os limites máximos e mínimos
IIQ = vol_amaciante["Volume"].quantile(0.75) - vol_amaciante["Volume"].quantile(0.25)
limite_superior = vol_amaciante["Volume"].quantile(0.75) + 1.5 * IIQ
limite_inferior = vol_amaciante["Volume"].quantile(0.25) - 1.5 * IIQ

# Adicionando a anotação dos limites superiores e inferiores de um boxplot
ax.annotate("Limite Superior", xy=(0, limite_superior), xycoords='data',  # coordenadas do ponto desejado
            bbox=dict(boxstyle="round", fc=CINZA5, ec=CINZA3),                          # caixa de texto
            xytext=(50, 0), textcoords='offset points',                                 # posição do texto
            arrowprops=dict(arrowstyle="->", color=CINZA3))                             # propriedades da seta

ax.annotate("Limite Inferior", xy=(0, limite_inferior), xycoords='data',
            bbox=dict(boxstyle="round", fc=CINZA5, ec=CINZA3),
            xytext=(50, 0), textcoords='offset points',
            arrowprops=dict(arrowstyle="->", color=CINZA3))

plt.show()
Copiar código
Saída:

alt-text: Boxplot criado com a biblioteca Seaborn e Matplotlib mostrando a distribuição do volume do amaciante da fábrica de produtos de higiene e limpeza para uma amostra de 1000 registros. O eixo x foi retirado por código. É possível notar no eixo y os intervalos de volume de 998,5 ml a 1001,5 ml. o boxplot está com a orientação vertical e a caixa com os quartis está na cor azul. É possível notar 2 anotações apontando para dois pontos próximos ao diagrama de caixa com as frases: limite inferior e limite superior

Como falamos durante a aula, os pontos fora do diagrama de caixa eram candidatos a outlier. Com o cálculo e exibição dos dados no boxplot, podemos observar que os pontos mais próximos da caixa, segundo os cálculos, ainda estão dentro dos padrões de aceitação.

A prática é sempre muito importante para fixar o conteúdo, ainda mais de um assunto tão importante que é o de visualização de dados. A análise de dados por meio de recursos visuais facilita a interpretação das pessoas sobre os dados e apresenta de maneira simples e direta o que eles representam e quais insights podemos adquirir nessa forma de exploração dos dados.

Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é extremamente importante para o seu crescimento dentro da carreira de dados. Portanto, busque realizar os exercícios propostos e veja como isso pode te ajudar a progredir em suas habilidades em visualização de dados.

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.

## Aula 05
### Desafio: gráficos de distribuição de dados para duas variáveis numéricas e/ou categóricas  
Vamos praticar a criação de gráficos de distribuição de dados para duas variáveis, numéricas e/ou categóricas. Para a prática, vamos trabalhar com duas base de dados diferentes: a primeira será um dataset com as notas de 3 turmas do curso de Data Visualization da plataforma de cursos de tecnologia fictícia que utilizamos em uma de nossas atividades, e a segunda será o dataset das medidas da caixa de sabão em pó da fábrica de produtos de higiene e limpeza que utilizamos durante essa aula, que está disponível no github do projeto.

Neste desafio, a missão é construir as visualizações que respondam aos questionamentos que compartilharemos aqui abaixo:

Desafio 1: Baixe a base de dados com as notas das turmas de Data Visualization e crie o violinplot, buscando interpretar as diferenças entre cada uma delas e documentando os seus achados. Sinta-se livre para adicionar alguns dos recursos que aprendemos ao longo do curso, como anotações, textos e figuras.

Desafio 2: Crie o gráfico de dispersão que distribua as medidas de comprimento e largura da amostra B. Desenhe no gráfico as linhas de rejeição para os itens em que o valor de comprimento e largura seja acima de 2% ou abaixo do valor de 20 cm e 5 cm, respectivamente.

Sinta-se livre para adicionar alguns dos recursos que aprendemos ao longo do curso, como anotações, textos e figuras.

Caso precise de ajuda, uma opção de solução da atividade estará disponível na seção “Opinião da pessoa instrutora”.

OBS: Caso ainda não tenha baixado o notebook dos desafios aproveite para baixá-lo agora. Ele possui as células e textos para você construir suas soluções e pode te ajudar a verificar seus códigos. Você pode baixar ele para resolver as atividades e desafios testando os seus conhecimentos até o momento.  

### Opinião do instrutor

Podem existir diversas formas de solucionar uma questão. Apresentamos abaixo uma sugestão de solução para cada problema, mas podem haver outras formas.

Desafio 1: Para o primeiro desafio vamos criar o violin plot e adicionar um texto com algumas observações na leitura do gráfico.

Importando os dados
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

notas = pd.read_csv("notas.csv")
notas.head()
Copiar código
Gerando o gráfico
# Área do gráfico e tema da visualização
fig, ax = plt.subplots(figsize=(10,5))
fig.subplots_adjust(right = 0.7)
sns.set_theme(style="whitegrid")

# Gerando o violinplot das notas
ax = sns.violinplot(data = notas, x = "Turma", y = "Nota", palette = "vlag_r")

# Personalizando o gráfico
plt.suptitle('Distribuição das notas das turmas de Data Visualization\n(100 alunos cada)', size=18, color=CINZA1, ha = 'left', x = 0.1, y = 1.05)
ax.set_xlabel('')
ax.set_ylabel('Notas (0-100)', fontsize = 14)
ax.xaxis.set_tick_params(labelsize=12, labelcolor = CINZA2)
ax.yaxis.set_tick_params(labelsize=12, labelcolor = CINZA2)
sns.despine(bottom=True)

# Criando uma lista com as medianas de cada turma
mediana = []
for i in range(1,4):
  mediana.append(notas.query(f"Turma == 'Turma {i}'").Nota.median())  

# Texto explicativo
ax.text(2.6, 60,
         'O gráfico acima mostra a distribuição dos valores entre\n'
         'três turmas do curso de Dataviz: $\\bf{Turma\ 1}$, $\\bf{Turma\ 2}$ e $\\bf{Turma\ 3}$.\n\n'
         'A $\\bf{Turma\ 1}$ apresenta uma distribuição aproximadamente normal,\n'
         f'com a mediana de {mediana[0]} e uma variabilidade moderada.\n\n'
         ' A $\\bf{Turma\ 2}$ mostra uma distribuição mais estreita, com a mediana\n' 
         f'de {mediana[1]} e uma variabilidade menor.\n\n'
         'Enquanto isso, a $\\bf{Turma\ 3}$ possui uma distribuição mais assimétrica,\n'
         f'com a mediana de {mediana[2]} e uma variabilidade maior em relação aos outros grupos.',
         fontsize=10, linespacing=1.45, color=CINZA2)

plt.show()
Copiar código
Saída:

alt-text: Violin plot criado com a biblioteca Seaborn e Matplotlib mostrando a distribuição das notas das turmas de Data Visualization da plataforma de cursos. É possível notar no eixo x as três turmas exibidas: Turma 1, Turma 2 e Turma 3. Os valores do eixo y variam de 10 em 10, partindo de 50 até 100 para as notas de Dataviz. Temos 3 violinplots diferentes representando a curva de distribuição e boxplot de cada turma. Cada desenho tem uma cor diferente. No lado direito do gráfico temos um texto  gerado pelo ax.text() explicando mais sobre os dados representados

Desafio 2: Para o primeiro desafio vamos selecionar os dados de comprimento e largura da amostra B e desenhar o gráfico de dispersão. Vamos também adicionar as linhas de rejeição em nosso gráfico.

Importando e tratando os dados
# Importando a base de dados dos volumes de um amaciante em 1000 amostras realizadas
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df_medidas = pd.read_csv("https://raw.githubusercontent.com/afonsosr2/dataviz-graficos/master/dados/medidas_sabao_em_po.csv")
df_b = df_medidas.query('amostra == "B"')[["comprimento", "largura"]]

df_b.head()
Copiar código
Gerando o gráfico
# Área do gráfico e tema da visualização
fig, ax = plt.subplots(figsize=(10,5))
sns.set_theme(style="white")

# Definindo as cores do gráfico e a porcentagem de rejeição
cores = [VERMELHO1, LARANJA1, AZUL2]
pct = 0.02

# Mapeando as cores para a faixa requisitada (2%)
rejeita_comp = [True if (c > 20*(1+pct) or c < 20*(1-pct)) else False for c in df_b["comprimento"]]
rejeita_larg = [True if (a > 5*(1+pct) or a < 5*(1-pct)) else False for a in df_b["largura"]]
map_cores = np.where(rejeita_comp, cores[0], np.where(rejeita_larg, cores[1], cores[2]))

# Gerando o gráfico de dispersão
ax = sns.scatterplot(data = df_b, x="comprimento", y = "largura", color = map_cores)

# Personalizando o gráfico
plt.suptitle('Distribuição das medidas da caixa de sabão em pó (amostra B de 200 registros)', size=14, color=CINZA1, ha = 'right', x = 0.9, y = 1)
ax.set_xlabel('Comprimento (cm)', fontsize = 12)
ax.set_ylabel('Largura (cm)', fontsize = 12)
ax.yaxis.set_tick_params(labelsize=10, labelcolor = CINZA2)
ax.xaxis.set_tick_params(labelsize=10, labelcolor = CINZA2)
sns.despine()

### Desenhando as linhas verticais com os limites mínimos e máximo de altura desejada
ax.text(20.15, 5.1, 'Limite máximo de largura', fontsize=12, color = CINZA2, ha="left", va = "bottom")
plt.axhline(y = 5 * (1 + pct), color = CINZA4, linestyle='--')
ax.text(20.15, 4.9, 'Limite mínimo de largura', fontsize=12, color = CINZA2, ha="left", va = "top")
plt.axhline(y = 5 * (1 - pct), color = CINZA4, linestyle='--')

plt.show()
Copiar código
Saída:

alt-text: Gráfico de dispersão criado com a biblioteca Seaborn e Matplotlib mostrando a distribuição de 200 registros das medidas da caixa de sabão em pó da amostra de nome B da fábrica de produtos de higiene e limpeza. É possível notar no eixo x os intervalos de comprimento partindo de 19,90 até 20,20 cm. Os valores do eixo y, com os intervalos de largura, partem do valor de 4,85 até 5,15. Temos pontos na cor azul e laranja. Os pontos em azul representam os valores das medidas cujo comprimento e largura estão dentro da faixa de aceitação de 2%, já os pontos em laranja representam os valores acima ou abaixo da faixa de aceitação de largura. É possível notar no gráfico duas linhas horizontais tracejadas cinzas que cortam o eixo y em 5,10 e 4,90 escrita limite máximo de largura e limite mínimo de largura, respectivamente.

A prática é sempre muito importante para fixar o conteúdo, ainda mais de um assunto tão importante que é o de visualização de dados. A análise de dados por meio de recursos visuais facilita a interpretação das pessoas sobre os dados e apresenta de maneira simples e direta o que eles representam e quais insights podemos adquirir nessa forma de exploração dos dados.

Compartilhar os seus conhecimentos e as práticas que vem desenvolvendo nesse ponto é extremamente importante para o seu crescimento dentro da carreira de dados. Portanto, busque realizar os exercícios propostos e veja como isso pode te ajudar a progredir em suas habilidades em visualização de dados.

Se você tiver alguma dúvida, você pode usar o fórum ou o discord da Alura.