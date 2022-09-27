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

A coluna ano está representando um **float**, precisamos realizar a conversão para **int** e apagar os anos zerados.

```
df['Year'] = df['Year'].astype(int)
df.drop(df[df['Year'] == 0].index, inplace = True)
```

Nesse momento terminamos nossa fase de tratamento dos dados, e agora iremos começar a agrupar as informações de maneira relevante para conseguirmos ter 'insights' com as informações disponíveis.

Vamos visualizar os 5 primeiros resultados da nossa tabela.

![display_df_head](/images/display_df_head.png/)

Agora nosso dataframe está bem mais intuitivo e compreensivo! Vamos identificar quais são as plataformas, publisher, genêro e ano que mais venderam, para isso é necessário criar cada agrupamento desejado de maneira separada e somar os valores.

![groupby_columns](/images/groupby_columns.png/)

Agora iremos análisar cada grupo criado, realizar a criação de gráficos e entender o que cada análise pode mostrar através de dados.
#
Análise das 5 plataformas mais vendidas.

![line_graph_platform](/images/line_graph_platform.png/)

Podemos notar que o PS2 foi o console mais vendido, com pouca diferença do segundo colocado que foi o Xbox! Em seguida temos Wii, PS3 e DS.
#
Análise das 5 publisher's mais vendidas.

![line_graph_publisher](/images/line_graph_publisher.png/)

A Nintendo foi a publisher mais vendida no período da análise, tendo mais que o dobro de número de vendas do segundo colocado, Eletronic Arts!
#
Análise dos 5 genêros mais vendidos.

![line_graph_genre](/images/line_graph_genre.png/)

Em 1º lugar com o maior número de vendas temos o genêro Action! Os genêros, Sports e Shooter, Platform e Role-Playing possuem pouca diferença de vendas globais!
#
Análise de todos os anos.

![line_graph_year](/images/line_graph_year.png/)

Podemos notar um gráfico crescente ao longo dos anos, poucas vendas globais do ano 1980 até o ano 1995 e apartir disso as vendas aumentam bastante! Sendo o ano de 2008 com o maior número de vendas globais! 
#
