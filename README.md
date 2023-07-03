# Project-Best-Selling-Gaming-Consoles-Dataset

# Sobre o Projeto
### Estou simulando ser um funcionário d


# Passo 1: Importei todas a blibliotecas que vou utilizar.

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import plotly.express as px

# Passo 2: Importei o arquivo csv para dentro de uma variável chamada dataset,
# usando a biblioteca Pandas, no lugar do comando sep, pode usar o delimiter, para separar por ",".
```python
dataset = pd.read_csv("best_selling_game_consoles.csv", sep =',')
```

# Passo 3: Abrir o dataset no python usando o comando DISPLAY.

display(dataset)



# Passo 4: Abrir o dataset usando o comando head(10), para exibir as 10 primeiras linhas do dataframe.
```python
#Passo 4: Abrir o dataset usando o comando head(10), para exibir as 10 primeiras linhas do dataframe.
display(dataset.head(10))
```
![image](https://github.com/AndersonSantos1979/Project-Best-Selling-Gaming-Consoles-Dataset.ipynb/assets/75112037/4ed91b29-6a19-43b7-a591-6c88adceec61)

# Passo 5: Mostrar o dataset somente o nome dos colunas, usar o comando ISNA(), 
# apresenta linhas nulas, linhas sem informaçõa. e o camando SUM() soma todos esses compos nulos.

print(dataset.isna().sum())


# Passo 6: Mostra informações resumidas do dataset, como quantidade de colunas, tipos de variáveis,
# quantidade de linhas e quantidade de linhas não nulas.
display(dataset.info())

# Posso 7: Aplicando o comando DESCRIBE(), para apresentar um resumo de informações sobre o dataset.

display(dataset.describe())

# Passo 8: Criei uma variável VENDAS_COMPANY, vai receber o total de vendas por companhia usando o comandos GROUPBY e SUM.

vendas_company = dataset[["Company","Units sold (million)","Console Name"]].groupby("Company").sum()
display(vendas_company)

# Passo 9: Criei uma variável MEDIA_COMPANY, vai receber a média de vendas por companhia usando
# o comandos GROUPBY e SUM. Usei o comando ROUD(), para arrendor com 2 digitos depois da "," o resultado apresentado.
media_company= dataset[["Company","Units sold (million)"]].groupby("Company").mean()
media_company = round(media_company,2)
display(media_company)

# Passo 10: Transformação do dados dentro da várialvel Vendas_company em formato de dicionário, usando o comando TO_formato.       
vendas_company = vendas_company.to_dict()
display(vendas_company)



# Passo 11: Colacando as informações do venda_company em duas lista, separadas

labels = []
values = []

for data in vendas_company['Units sold (million)']:
    labels.append(data)
    values.append(vendas_company['Units sold (million)'][data])
    
    

#grafico = px.bar(media_company, x= "Company", y="Units sold (million)",)
#grafico.show()

# Passo 12: Criação do grafico de pizza com as informações contida no venda_company. usando a biblioteca Plotly express.
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



# Passo 13: Criando um novo gráfico de Barras, ficou  com a informações legiveis e melhor visualização 
# usando a biblioteca Plotly express.

grafico = px.bar(vendas_company, x= "Company",y= "Units sold (million)",
                 title= "TOTAL DE VENDAS POR COMPANHIA",text_auto="Type")

grafico.show()

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
