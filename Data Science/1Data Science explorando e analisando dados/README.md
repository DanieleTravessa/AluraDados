# Dados
Repositório relacionado às aulas de Dados da Alura

# Data Science: explorando e analisando dados

Essa pasta tem os materiais de estudo relacionados ao terceiro curso da formação Avançada em Dados.

A estrutura de arquivos e da documentação é dada da seguinte forma:  
- 3 Arquivos com o nome do curso e semana contendo:  
1. Links para materiais de apoio mencionados no curso  
2. Exemplos dados nas áreas Para Saber Mais  
3. Anotações diversas
- Outros materiais  
4. Links dos vídeos das aulas  
5. Notebooks das Aulas para uso no Google Colab ou com JunyperNotebook  
6. Caderno de Exercícios no formato de Notebook Python

## Encontre os links dos vídeos das aulas aqui:
[Aula 1]()
[Aula 2]()
[Aula 3]()
[Aula 3]()
[Aula 4]()

## Conteúdos - O que aprendemos  
**Aula 1**  
Importar a biblioteca pandas para a análise exploratória dos dados;
Ler um conjunto de dados no formato .csv, compreendendo a sua estrutura;
Fazer upload de arquivos para o Google Colab e reconhecer a importância de verificar se a máquina virtual está ativa ou se precisa ser reiniciada;
Renomear as colunas de um DataFrame e rodar códigos para contagem e descrição dos dados;
Identificar o que é uma Series e DataFrame;
Melhorar a visualização das informações e gerar os primeiros visuais para observação dos dados.  

**Aula 2**  
Trabalhar com o método query() para filtrar linhas de um DataFrame com base em uma expressão;
Realizar o agrupamento dos dados a partir de uma coluna por meio do método groupby();
Extrair dados filtrando uma única coluna;
Modificar os “bins” (intervalos) de um histograma verificando o seu comportamento;
Identificar as diferentes bibliotecas de visualização, como Matplotlib e Seaborn;
Inserir textos no notebook para explicar os dados e criar um storytelling de nossas análises.    

**Aula 3**  
Identificar o tipo de variável observando seu conteúdo;
Diferenciar uma variável categórica (qualitativa) nominal de uma ordinal;
Compreender o que é uma variável quantitativa contínua e discreta e visualizar a diferença entre intervalos.  
   
**Aula 4**  
Comparar categorias gerando um visual de gráfico de barras pelo barplot() e countplot();
Transformar uma Series em DataFrame pela função to_frame() e criar um DataFrame por meio de um dicionário pela classe pd.DataFrame();
Compreender que para comparação de dados o uso de áreas é bem complexo e contra-indicado, pois o conceito de área não é tão natural para visualização dos dados;
Compreender que em visualização de dados devemos colocar como foco a mensagem que queremos passar, adequando-a ao tipo de visual correspondente;
Ajustar os dados para construir um visual de acordo com o que queremos informar.  

**Aula 5**  
Ajustar as escalas de um gráfico aproveitando o espaço e melhorando a visualização dos dados;
Ordenar os dados de um gráfico dando uma coesão a representação desses dados;
Alterar cores e tons de um gráfico destacando elementos e melhorando a sua estética visual;
Representar um gráfico de colunas com dados absolutos e relativos (porcentagem).  

**Aula 6**  
Diferenciar as medidas de tendência central e compreender o que cada uma representa;
Utilizar a biblioteca Numpy para cálculos de média, mediana e desvio padrão de listas;
Reconhecer a importância de trabalhar com as medidas de tendência central junto a dispersão de dados, a fim de comparar também como estes dados estão distribuídos;
Comparar diferentes registros e investigar as diferenças entre eles visualmente por meio das medidas de tendência central e gráficos de distribuição de dados.

Para visitar o projeto relacionado à esse curso, siga esse [link]().  
-------------------------------------------------------------------------------------------
Estrutura de Organização das tarefas  
-> Gravação:  
    1. Software Local: Aulas gravadas em ciclos de aulas, pausando a quebra por aula.  
    - Subir para o YouTube com o código da semana, o nome do curso e o número da aula.  
    - Organizar as aulas de um mesmo curso em Formato de Playlist.  
    2. Vimeo: Aulas gravadas em ciclos de 2h ou 30 min, sem quebra definida.  
-> Links e arquivos:  
    - Revisitar o material para copiar e documentar links, códigos, exemplos, notebooks e material de apoio.  
-> Reassistir a aula a partir da gravação, garantindo o sucesso da gravação e verificando a possível ausência de alguma.  
-> Prática  
    - Fazer todo o ciclo de exercícios e práticas.  
-> Gabarito:  
    - Depois da prática consultar (e documentar) as soluções a partir dos campos 'Faça como eu fiz' ou 'Opnião do Instrutor'.  

----------------------------------------------------------
**Comandos úteis Git**  
*Ordem de Execução*  

git init  
git config --list  
*Se necessário:*  
git config --global user.name "Daniele Travessa" 
git config --global user.email "danieletravessa@gmail.com"   
*Em sequência:*  
git remote add origin https://github.com/DanieleTravessa/BoticarioDesenvolve_Aulas.git  
git checkout -b <branch nova>  
git add .  
git commit -m ''  
git push -u origin <branch nova>  

