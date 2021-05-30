# :movie_camera: **Serviços de Streaming**

Os dados são obtidos dos catálogos das plataformas. Alguns serviços em API realizam essa obtenção, como Guidebox, Gracenote e GoWatchit, mas não é especificado na plataforma qual o método utilizado para obtenção dos dados.

## :school_satchel: **Introdução/Contexto Sócio-histórico**

É fácil observar que a pandemia alterou e muito nossas práticas cotidianas. O uso de máscaras e o cuidado com a etiqueta respiratória são exemplos claros e facilmente observáveis, uma vez que se relacionam diretamente a medidas sanitárias que visam o combate à pandemia. No entanto, algumas mudanças secundárias nos nossos hábitos podem ser observadas.
O consumo de entretenimento via streaming é algo que tem aumentado ano após ano. Seja no segmento fonográfico ou audiovisual, o mercado teve de se ajustar ao novo comportamento de consumo do público. Gigantes da indústria, como Disney e Amazon, lançaram seus próprios serviços para competir pelo mercado. E esse mercado entrou em franca expansão com a pandemia da COVID-19.
Conforme medidas restritivas eram tomadas por todo o mundo, o público viu no consumo de streaming uma das poucas alternativas ainda viáveis para o lazer. Conforme estudo da Ofcom noticiado pela BBC (https://www.bbc.com/news/entertainment-arts-53637305), o Reino Unido registrou um aumento de 12 milhões de usuários em serviços de streaming, além de um aumento no tempo que esses consumidores passavam assistindo conteúdos nesses serviços. Já segundo a Motion Picture Association (https://www.marketwatch.com/story/global-streaming-subscriptions-top-1b-during-covid-2021-03-18), em 2020 o número total de subscrições a serviços de streaming ao redor do mundo chegou a 1.1 bilhões de utilizadores, enquanto receitas de bilheteria nos cinemas seguiram em derrocada devido às medidas de isolamento.
Por conta do aumento da demanda por conteúdos via streaming, é natural que a oferta acabe se diversificando em meio à disputa por market shares. Dessa forma, cada serviço de streaming oferece diferentes conteúdos e disputam entre si para disponibilizar aqueles que melhor atenderão seu público. Do ponto de vista do consumidor, é interessante portanto saber qual serviço possui os conteúdos que melhor se adequem às suas preferências.
Pensando nisso, concebemos este presente projeto como uma forma de analisar e mostrar os dados obtidos como forma de auxiliar a análise sobre os principais serviços de streaming disponíveis atualmente.

## 🧱: **Estrutura**
Os datasets utilizados foram recolhidos do kaggle, os dados são open source e os autores serâo referenciados.

- [tv_shows.csv](https://www.kaggle.com/ruchi798/tv-shows-on-netflix-prime-video-hulu-and-disney)- Upload feito por Ruchi Bhatia | Dataset contèm dados referentes a varias plataformas de streaming (Netflix,Hulu Prime Video e Disney+)

- [netflix_titles.csv](https://www.kaggle.com/shivamb/netflix-shows)- Upload feito por Shivam Bansal | Dataset contèm dados referentes a plataforma de streaming da netflix até 2019


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
- Erica De Brito- 

