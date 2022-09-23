# Análise de dados - Venda de videogames

Nesse projeto iremos trabalhar com o conjunto de dados [Video Game Sales](https://www.kaggle.com/datasets/gregorut/videogamesales) dísponivel no [Kaggle](https://www.kaggle.com/datasets), uma excelente plataforma para encontrar datasets gratuitos e utiliza-lós para a manipulação de dados!

Ao abrir o arquivo **_vgsales.csv_** as informações não são de facil entendimento, a estrutura das informações parece desorganizada.

![raw_vgsales](/images/raw_vgsales.png/)

Nesse projeto será utilizado o [Google Collab](https://colab.research.google.com/) para realizar a análise em questão.
Para iniciar, devemos importar a biblioteca pandas, que é uma biblioteca bastante utilizada para a análise de dados.

```
import pandas as pd
```

Agora precisamos carregar nosso dataset no Python com a utilização da biblioteca pandas

```
df = pd.read_csv('vgsales.csv', sep=',')
```

Pronto! Nesse momento conseguimos interpretar as informações do dataframe de maneira mais clara e objetiva.
![display_df](/images/display_df.png/)

Agora temos acesso a várias informações, nome, plataforma, ano. Nesse projeto iremos descartar algumas colunas que não serão relevantes para a análise em questão.

Não iremos trabalhar com as colunas: **_Rank, NA_Sales, EU_Sales, JP_Sales, Other_Sales_**. Portanto iremos removê-las.

```
df = df.drop('Rank'       , axis=1)
df = df.drop('NA_Sales'   , axis=1)
df = df.drop('EU_Sales'   , axis=1)
df = df.drop('JP_Sales'   , axis=1)
df = df.drop('Other_Sales', axis=1)
```
