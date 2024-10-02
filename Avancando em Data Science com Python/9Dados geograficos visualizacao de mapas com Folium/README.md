# Dados
Repositório relacionado às aulas de Dados da Alura

# Dados geográficos: visualização de mapas com Folium

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
Ler dados georreferenciados usando a biblioteca GeoPandas;
Inserir e controlar de forma interativa camadas bases de um mapa usando a biblioteca Folium;
Extrair contornos agrupados por região usando o método dissolve();
Inserir camadas de contorno de mapas usando o método GeoJson() da biblioteca Folium.    

**Aula 2**  
Verificar quais pontos geográficos estão contidos dentro de uma região com o método within;
Criar mapas de calor para identificar a concentração de pontos em regiões;
Personalizar a visualização de um HeatMap;
Criar mapas de calor animados com base em um período temporal;
Adicionar tooltips informativos em visualizações usando o Folium.    

**Aula 3**  
Criar marcadores em uma visualização de mapas usando o Folium;
Construir pop-ups para adicionar informações ao mapa e deixá-lo mais interativo;
Personalizar os marcadores com ícones e cores para representar uma informação de forma visual;
Agrupar marcadores em clusters para conseguir representar milhares de elementos em uma única visualização sem perda de desempenho.  
   
**Aula 4**  
Verificar quais pontos geográficos de um GeoDataFrame estão dentro de cada região contida em outro GeoDataFrame com o método within;
Extrair informações estatísticas agregadas com o uso do groupby e agg;
Construir mapas coropléticos com informações numéricas representadas por cores com o método Coropleth;
Inserir tooltips contendo informações estatísticas em regiões geográficas usando o GeoJsonTooltip.  

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

