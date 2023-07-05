
# Anderson Santos
<sub>Engenheiro de Dados JR.</sub>

Bacharelando em Ciência da Computação pela Universidade Ibirapuera (UNIB), com bons conhecimentos em  SQL e Python. Construo painéis e relatórios analíticos, em Python e Power BI, desde o levantamento de requisitos até a publicação online e análise dos dados, utilizando técnicas de Data Storytelling em busca da melhor solução para os clientes.

Estou em constante busca pelo aprimoramento dos conhecimentos em Python, principalmente em bibliotecas como: Pandas, Numpy e outras que possam ser importante para analise de dados. Desta forma, consigo auxiliar a tomada de decisão através de boas estórias e análises! Além disso, possuo experiência há 11 como analista de suporte em algumas empresas de TI entre elas a Keyrus Brasil uma cia no ramo de dados.

**Experiências em:** Python, Análise de Dados.


## Project-Best-Selling-Gaming-Consoles-Dataset 1972-2020
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/a19d7aa8-3a04-4e4d-98c9-a4793f41703b)


##### Sobre o Projeto
Estou simulando uma análise de dados sobre um projeto que visa identificar quais consoles de video game foram mais vendidos, contudo, tive a oportunidade de tirar alguns insights,
ao logo da descrição do projeto vou mostrando a forma que cheguei até algumas conclusões. 

##### Passo 1: Importei todas a blibliotecas que vou utilizar.
```Python import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import plotly.express as px
```

##### Passo 2: Importei o arquivo csv para dentro de uma variável chamada dataset,
```python
# Usando a biblioteca Pandas, no lugar do comando sep, pode usar o delimiter, para separar por ",".

dataset = pd.read_csv("best_selling_game_consoles.csv", sep =',')
```
##### Passo 3: Abrir o dataset no python usando o comando DISPLAY.
```Python
display(dataset)
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/20b85d72-1821-43eb-b081-14b10584771c)


##### Passo 4 :Excluir uma coluna do dataset que não tinha fazia sentido para nossa análise.
```Python
# Usando a função DROP do Pandas passando o paramêtro axis= 1 que signigica coluna, assim excluí a coluna Remarks,
dataset.drop('Remarks',axis=1)

```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/9af921a8-75f9-4543-8724-bacda7f05d8d)




##### Passo 5: Abrir o dataset usando o comando head(10), para exibir as 10 primeiras linhas do dataframe.
```python
#Passo 4: Abrir o dataset usando o comando head(10), para exibir as 10 primeiras linhas do dataframe.
display(dataset.head(10))
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/017ec0b8-fb97-4020-b1d4-3ea202c7251e)


##### Passo 6: Mostrar o dataset somente o nome dos colunas, usar o comando ISNA(), 

```python
# apresenta linhas nulas, linhas sem informaçõa. e o camando SUM() soma todos esses compos nulos.
print(dataset.isna().sum())
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/87d7e11a-2ba5-458b-8ab0-4abfadb9c4a6)



##### Passo 7: Mostra informações resumidas do dataset, como quantidade de colunas, tipos de variáveis,
```Python
# quantidade de linhas e quantidade de linhas não nulas.
display(dataset.info())
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/b32bf6df-334c-4918-bfd8-cd9026c525f2)


##### Posso 8: Aplicando o comando DESCRIBE(), para apresentar um resumo de informações sobre o dataset.
```Python
display(dataset.describe())
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/cedab3b2-34b9-41c6-85e5-7460c8cddd3c)

##### Passo 9: Criei uma variável VENDAS_COMPANY, vai receber o total de vendas por companhia usando o comandos GROUPBY e SUM.
```Python
vendas_company = dataset[["Company","Units sold (million)","Console Name"]].groupby("Company").sum()
display(vendas_company)
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/8825852e-905e-4f9b-a4d4-95205bffa91c)

##### Passo 10: Criei uma variável MEDIA_COMPANY, vai receber a média de vendas por companhia usando
```Python
# o comandos GROUPBY e SUM. Usei o comando ROUD(), para arrendor com 2 digitos depois da "," o resultado apresentado.
media_company= dataset[["Company","Units sold (million)"]].groupby("Company").mean()
media_company = round(media_company,2)

display(media_company)
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/c1b67913-0019-463c-b7e6-031cad8d0a79)

##### Passo 11: Transformação do dados dentro da várialvel Vendas_company em formato de dicionário, usando o comando TO_formato.       
```Python
vendas_company = vendas_company.to_dict()
display(vendas_company)
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/8f848a15-8ec2-485a-91ce-b7b5428be40e)


##### Passo 12: Colacando as informações do venda_company em duas lista, separadas
```Python
labels = []
values = []

for data in vendas_company['Units sold (million)']:
    labels.append(data)
    values.append(vendas_company['Units sold (million)'][data])
    
```

##### Passo 13: Criação do grafico de pizza com as informações contida no venda_company. usando a biblioteca Plotly express.
```Python
# No entanto as informações ficaram inelegiveis.

# Criando conjunto de dados

labels=list(labels)
sizes=values        


# Criando a representação da área da plotagem

fig1, ax1 = plt.subplots(figsize=(12,7))

# Criando o gráfico

ax1.pie(sizes,labels=labels,autopct='%1.0f%%' ,shadow=True, startangle=90)

# Opção para gráficar ficar em circulo
ax1.axis('equal')

# Apresenta o gráfico
print(" Total de vendas de console por empresa")
plt.show()

```

##### Passo 13: Criando um novo gráfico de Barras, ficou  com a informações legiveis para melhor visualização das infomações.
```Python
# usando a biblioteca Plotly express.

grafico = px.bar(vendas_company, x= "Company",y= "Units sold (million)",
                 title= "TOTAL DE VENDAS POR COMPANHIA",text_auto="Type")

grafico.show()
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/200f783c-d4bf-4ff2-8994-2fdba5d91069)


# Passo 14: Criando um gráfico com as 5 principais empresas que mais venderam console.

labels =('Atari','Microsoft','Nintendo','Sega','Sony')

sizes= [33, 185, 883,78.40, 589.09]        


# Criando a representação da área da plotagem

fig1, ax1 = plt.subplots(figsize=(6,6))

# Criando o gráfico

ax1.pie(sizes,labels=labels,autopct='%1.0f%%' ,shadow=True, startangle=70.50)

# Opção para gráficar ficar em circulo
ax1.axis('equal')


# Apresenta o gráfico
print(" Total de vendas de consoles por empresa")
plt.show()



#total = tabela[["Company", "Units sold (million)"]]
# Passo 16: ESSE DATASET VENDA_CAMPANY AS INFORMAÇÕES AGRUPADO PELA COLUNA "RELEASED YEAR" E CONTA O VALORES.
vendas_company = dataset[['Console Name',"Company","Type","Units sold (million)",
                            'Released Year']].groupby("Released Year",as_index=False).value_counts()
display(vendas_company)


# Passo 17: Usando o comando LOC, para exiber as informações de todos os consoles vendidos pela Nitendo.
vendas_Nintendo = dataset.loc[(dataset["Company"] == "Nintendo")]
                            
display(vendas_Nintendo)



# Passo 18: Usando a biblioteca Plotly Exepress para criar gráfico de barras usando alguns 
# paramentros como color, text_auto e title.
grafico = px.bar(vendas_Nintendo, x="Console Name",y= "Units sold (million)",color = "Type", text_auto=True,
                 title = "VENDAS TOTAL DA NITENDO POR CONSOLE")
# Usando comoando show para exibir o gráfico.
grafico.show()

# Passo 19: Usando o comando LOC, para exiber as informações de todos os consoles vendidos pela Sony.
vendas_Sony = dataset.loc[(dataset["Company"] == "Sony")]
                            
display(vendas_Sony)

# Passo 20: Usando a biblioteca Plotly Exepress para criar gráfico de barras usando alguns 
# paramentros como color, text_auto, title e Barmode.
grafico = px.bar(vendas_Sony, x="Console Name",y= "Units sold (million)",color = "Type",
                 title = "VENDAS TOTAL DA SONY POR CONSOLE",text_auto='Type',barmode='group')
# Usando comoando show para exibir o gráfico.
grafico.show()

# Passo 21: Usando o comando LOC, para exiber as informações de todos os consoles vendidos pela Microsoft.
vendas_Microsoft = dataset.loc[(dataset["Company"] == "Microsoft")]
                            
display(vendas_Microsoft)

# Passo 26: Colocando um dataset formato parquet em uma váriavel chamada Vendas_company e exibindo com comando Display.

vendas_company = dataset[['Company',"Console Name","Type","Units sold (million)",
                            'Released Year']].groupby("Company",as_index=False).value_counts()
display(vendas_company)
type(vendas_company)

# Passo 23: Usando o comando LOC, para exiber as informações de todos os consoles vendidos pela Sega.
vendas_Sega = dataset.loc[(dataset["Company"] == "Sega")]
                            
display(vendas_Sega)

# Passo 24: Usando a biblioteca Plotly Exepress para criar gráfico de barras usando alguns 
# paramentros como color, text_auto, title e Barmode.

grafico = px.bar(vendas_Sega, x="Console Name",y= "Units sold (million)",color = "Type",
                 title = "VENDAS TOTAL DA SEGA POR CONSOLE ",text_auto= True,barmode="relative")
# Usando comoando show para exibir o gráfico
grafico.show()

# Tipo de arquivo com extesão PARQUET

# Passo 25:  Transformar um arquivo csv em parquet usando comando TO_

dataset.to_parquet('C:/Users/Keyrus/Documents/Scripts Python/Atividades/best_selling_game_consoles.parquet')

# Passo 26: Colocando um dataset formato parquet em uma váriavel chamada Vendas_company e exibindo com comando Display.

vendas_company = dataset[['Company',"Console Name","Type","Units sold (million)",
                            'Released Year']].groupby("Company",as_index=False).value_counts()
display(vendas_company)
type(vendas_company)
