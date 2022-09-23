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

Importante destacar: **Uma** venda global representa **um milhão**.
Agora temos acesso a várias informações, nome, plataforma, ano. Nesse projeto iremos descartar algumas colunas que não serão relevantes para a análise em questão.

Não iremos trabalhar com as colunas: **_Rank, NA_Sales, EU_Sales, JP_Sales, Other_Sales_**. Portanto iremos removê-las.

```
df = df.drop('Rank'       , axis=1)
df = df.drop('NA_Sales'   , axis=1)
df = df.drop('EU_Sales'   , axis=1)
df = df.drop('JP_Sales'   , axis=1)
df = df.drop('Other_Sales', axis=1)
```

É comum em conjunto de dados alguns valores encontrarem-se nulos ou vazios, nessa situação precisamos tratar esses dados para não influenciar na análise de forma negativa, nesse projeto iremos atribuir o valor 0 para os registros que estiverem nessas condições.

Primeiro verificamos se existem elementos nulos ou vazios.

```
df.isnull().values.any()
> True
```

Agora atribuimos o valor 0 para esses registros.

```
df = df.fillna(0)
```

Verificamos novamente se existem valores nulos.

```
df.isnull().values.any()
> False
```

Pronto, agora não existem mais valores nulos em nossa base de dados!

Qual será os cinco menores valores da coluna vendas globais?

![display_lowest_global_sales](/images/display_lowest_globalsales.png/)

Nesse projeto iremos descartar todas as vendas globais com **valores inferiores a 0,99** e arredondar os demais valores.

```
df.drop(df[df['Global_Sales'] <= 0.99].index, inplace = True)
df['Global_Sales'] = df['Global_Sales'].round(0).astype(int)
```

A coluna ano está representando um **float**, precisamos realizar a conversão para **int**.

```
df['Year'] = df['Year'].astype(int)
```
