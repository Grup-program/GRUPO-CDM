# :movie_camera: **Avaliação dos Serviços de Streaming Netflix, Disney+ e Prime Video.**

Os dados são obtidos dos catálogos das plataformas. Alguns serviços em API realizam essa obtenção, como Guidebox, Gracenote e GoWatchit, mas não é especificado na plataforma qual o método utilizado para obtenção dos dados.

## :school_satchel: *Contexto*

É fácil observar que a pandemia alterou e muito nossas práticas cotidianas. O uso de máscaras e o cuidado com a etiqueta respiratória são exemplos claros e facilmente observáveis, uma vez que se relacionam diretamente a medidas sanitárias que visam o combate à pandemia. No entanto, algumas mudanças secundárias nos nossos hábitos podem ser notadas. Um exemplo disso é o consumo de entretenimento via streaming. 

Seja no segmento fonográfico ou audiovisual, o mercado teve de se ajustar ao novo comportamento de consumo do público. Gigantes da indústria, como Disney e Amazon, lançaram seus próprios serviços para competir pelo mercado. E esse mercado entrou em franca expansão com a pandemia da COVID-19.

Conforme medidas restritivas eram tomadas por todo o mundo, o público viu no consumo de streaming uma das poucas alternativas ainda viáveis para o lazer. Conforme [estudo da Ofcom noticiado pela BBC](https://www.bbc.com/news/entertainment-arts-53637305), o Reino Unido registrou um aumento de 12 milhões de usuários em serviços de streaming, além de um aumento no tempo que esses consumidores passavam assistindo conteúdos nesses serviços. 

Já segundo a [Motion Picture Association](https://www.marketwatch.com/story/global-streaming-subscriptions-top-1b-during-covid-2021-03-18), em 2020 o número total de subscrições a serviços de streaming ao redor do mundo chegou a 1.1 bilhões de utilizadores, enquanto receitas de bilheteria nos cinemas seguiram em derrocada devido às medidas de isolamento.

Por conta do aumento da demanda por conteúdos via streaming, é natural que a oferta acabe se diversificando em meio à disputa por market shares. Dessa forma, cada serviço de streaming oferece diferentes conteúdos e disputam entre si para disponibilizar aqueles que melhor atenderão seu público. Do ponto de vista do consumidor, é interessante portanto saber qual serviço possui os conteúdos que melhor se adequem às suas preferências.

Pensando nisso, concebemos este presente projeto como uma forma mostrar os dados obtidos de maneira a ajudar o público a escolher melhor quais serviços assinar.
## 🧱: **Estrutura**
### **Os dados utilizados**
Os datasets utilizados foram recolhidos do kaggle, os dados são open source e os autores serâo referenciados.

- [tv_shows.csv](https://www.kaggle.com/ruchi798/tv-shows-on-netflix-prime-video-hulu-and-disney)- Upload feito por Ruchi Bhatia | Dataset contèm dados referentes a varias plataformas de streaming (Netflix,Hulu Prime Video e Disney+)

- [netflix_titles.csv](https://www.kaggle.com/shivamb/netflix-shows)- Upload feito por Shivam Bansal | Dataset contèm dados referentes a plataforma de streaming da netflix até 2019

Ao buscarmos dados para realizar o embasamento em nossa análise sobre os serviços de streaming encontramos diversos trabalhos semelhantes, mas cuja proposta não se destinava tanto ao consumidor. A maioria dos trabalhos com dados de streaming não instrumentalizam esses dados para o consumidor.

Um dataset que encontramos que melhor se adequou a nossa proposta foi o [dataset](https://github.com/ruch798/Movies-and-TV-shows) organizado por [Ruchi Bhatia](https://www.linkedin.com/in/ruchi798/) .

Bhatia é uma executiva associada em Colgate-Palmolive e embaixadora global em data science para Nvidia e HP. Analisamos como ela realizou o data scrapping:

### **Data Scrapping**

 No repositório disponibilizado por Bhatia podemos visualizar o código do programa utilizado para obter os dados dos serviços de streaming. Não foi uma tarefa tão fácil realizar essa análise, tendo sido necessário pesquisar um pouco sobre linguagem HTML. Isso porque o approach escolhido por Bhatia foi utilizar as informações fornecidas na página web do serviço [Reelgood](https://reelgood.com/about), um hub que reune o catálogo de serviços de streaming variados. Vejamos o código utilizado por Bhatia:

"print(\"Netflix TV shows\")\n",
        "records = []\n",
        "\n",
        "for i in range(0,501):\n",
        "  URL = \"https://reelgood.com/tv/source/netflix?offset=\" + str(i*50)\n",
        "  r = requests.get(URL, timeout=5)\n",
        "  soup = BeautifulSoup(r.text,'html.parser')\n",
        "  row = soup.find_all('tr',attrs={'class':'css-gfsdx9'})\n",
        "\n",
        "  for t in row:\n",
        "        title = t.find(attrs={'class':'css-1u7zfla e126mwsw1'}).text\n",
        "        year = t.find(attrs={'class':'css-1u11l3y'}).text\n",
        "        age = t.find(attrs={'class':'css-1u11l3y'}).findNext('td').text\n",
        "        IMDb = t.find(attrs={'class':'css-1u11l3y'}).findNext('td').findNext('td').text\n",
        "        rottenTomatoes = t.find(attrs={'class':'css-1u11l3y'}).findNext('td').findNext('td').findNext('td').text\n",
        "        records.append([title, year, age, IMDb, rottenTomatoes])\n",
        "  i =  i + 1\n",
        "\n",
        "df1 = pd.DataFrame(records) \n",
        "df1.rename(columns = {0:'Title', 1:'Year', \n",
        "                              2:'Age', 3:'IMDb', 4:'Rotten Tomatoes'}, inplace = True) \n",
        "df1['Netflix'] = 1\n",
        "df1['Hulu'] = 0\n",
        "df1['Prime Video'] = 0\n",
        "df1['Disney+'] = 0\n",
        "df1"

Basicamente, este programa analisa cada parte da página do catálogo Netflix presente no site Reelgood, na URL https://reelgood.com/tv/source/netflix?offset= . Em detalhes, analisemos as linhas do código:

"print(\"Netflix TV shows\")\n",
        "records = []\n",
        "\n",
        "for i in range(0,501):\n",
        "  URL = \"https://reelgood.com/tv/source/netflix?offset=\" + str(i*50)\n",
        "  r = requests.get(URL, timeout=5)\n",
        "  soup = BeautifulSoup(r.text,'html.parser')\n",
        "  row = soup.find_all('tr',attrs={'class':'css-gfsdx9'})\n",
        "\n",

Esta parte do código cria a lista denominada "Netflix TV shows", sendo preenchida por um looping (for) que terá um alcance (range) até 501, com a requisição de acesso à URL sendo realizada a cada 5 segundos. Como o código da página do Reelgood é em HTML, o comando BeautifulSoup utilizado transforma a informação obtida em HTML em formato próprio para o JSON. A variável row corresponde as fileiras em que estão os títulos do catálogo na página indicada, sendo identificada no código HTML com a classe css-1u11l3y. 

"  for t in row:\n",
        "        title = t.find(attrs={'class':'css-1u7zfla e126mwsw1'}).text\n",
        "        year = t.find(attrs={'class':'css-1u11l3y'}).text\n",
        "        age = t.find(attrs={'class':'css-1u11l3y'}).findNext('td').text\n",
        "        IMDb = t.find(attrs={'class':'css-1u11l3y'}).findNext('td').findNext('td').text\n",
        "        rottenTomatoes = t.find(attrs={'class':'css-1u11l3y'}).findNext('td').findNext('td').findNext('td').text\n",
        "        records.append([title, year, age, IMDb, rottenTomatoes])\n",
        "  i =  i + 1\n",
        "\n",

Dentro da fileira designada é realizado for que vai obter os dados a serem preenchidos. Podemos perceber que as informações estão identificadas com a mesma classe css-1u11l3y, e portanto é utilizado o comando findNext tantas vezes quanto se faz necessário para obter a informação desejada. O número de vezes que se usa o comando é relativo a ordem em que essas infomações se apresentam na página do Reelgood: primeiro temos o título, em seguido o ano e assim por diante. Por fim, para interromper o for, é redefinida a varável i para i +1.

"df1 = pd.DataFrame(records) \n",
        "df1.rename(columns = {0:'Title', 1:'Year', \n",
        "                              2:'Age', 3:'IMDb', 4:'Rotten Tomatoes'}, inplace = True) \n",
        "df1['Netflix'] = 1\n",
        "df1['Hulu'] = 0\n",
        "df1['Prime Video'] = 0\n",
        "df1['Disney+'] = 0\n",
        "df1"

Para colocar as informações no formato de data frame foram utilizados os comandos de Panda, criando as colunas "Title", "Year", "Age", "IMDB", "Rotten Tomatoes" de acordo com as variáveis anteriormente atribuídas.

Esse processo se repetiu para cada serviço de streaming, formando o dataset que usamos neste trabalho.


### Limpeza de dados

Os dados foram manejados de acordo com as nossas propostas: isolar cada serviço de streaming, agrupar as classificações indicativas e filtrar intervalos de notas no IMDB. Os códigos para limpeza dos dados podem ser verificados no arquivo do Jupyter Notebook.


## :page_with_curl: Dicionário de dados

| Nome da coluna    |   Conteúdos       
|-------------------|--------------------------------------------------------------------------------
|    Title          | Título dos filmes e series
|    Year           | Ano de Estreia dos filmes
|    Age            | Classificação por idades dos filmes e series
|    IMDB           | Classificação quantitativa pelo IMDB dos filmes e series 
|    Rotten Tomatoes| Classificação quantitativa pelo IMDB dos filmes e series
|    Netflix        | Valor sobre a existência de um determinado titulo na plataforma de streaming Netflix (1- possui; 0- não possui )
|    Hulu           | Valor sobre a existência de um determinado titulo na plataforma de streaming Hulu  (1- possui; 0- não possui )
|    Prime Video    | Valor sobre a existência de um determinado titulo na plataforma de streaming Prime Video  (1- possui; 0- não possui )
|    Disney         | Valor sobre a existência de um determinado titulo na plataforma de streaming Disney+  (1- possui; 0- não possui )
|    Type           | Valor de ser serie ou filme (1-Serie; 0-filme)
|    Director       | Diretor do filme ou serie


| Nome da Coluna    |  Conteúdos 
|-------------------|----------------------------------------------------------------------------------
|    Cast           | Elenco do título
|    Country        | País onde foi realizado
|    Date_added     | Data quando foi adicionado À plataforma
|    Release_year   | Ano de estreia
| Rating duration   | Duração do título

## :mag:*Referencias de pesquisa*

- [Deleting DataFrame row in Pandas based on column value](https://stackoverflow.com/questions/18172851/deleting-dataframe-row-in-pandas-based-on-column-value)

- [Create a Pie Chart of Pandas Series Values](https://datascienceparichay.com/article/create-a-pie-chart-of-pandas-series-values/)

- [Manipulação de colunas em um dataframe](https://www.youtube.com/watch?v=6NgyWKaP1ZU)

- [Construção Pie chart](https://medium.com/horadecodar/gr%C3%A1ficos-de-pizza-com-matplotlib-piechart-33ea9760ad87)

- [Remover colunas com pandas](https://www.alura.com.br/artigos/como-remover-linhas-e-colunas-no-pandas)

- [Parametros de costumização Pie chart](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.pie.html#matplotlib.pyplot.pie)

- [Guia de projeto de Data science](https://paulovasconcellos.com.br/como-criar-seu-primeiro-projeto-de-data-science-parte-2-de-2-cb9a2fe05eff)

- [Vizualização de data a partir de uma coluna](https://stackoverflow.com/questions/43549901/visualize-data-from-one-column)

- [Converter string de percentagem em float](https://stackoverflow.com/questions/25669588/convert-percent-string-to-float-in-pandas-read-csv)

## :construction_worker: *Colaboradores do Projeto*

- João Perdiz- 2020120187
- Pedro Bosco Lira- 2020100275
- Erica De Brito- 2020108454




