# Projeto Final de Análise de Dados

Desenvolvido por:

Paloma Avena palomaavena@gmail.com

Anne Ribeiro anne.asribeiro@gmail.com

## Contexto  

Este projeto consiste na criação de um banco de dados e análise destes dados de desmatamento e CO2 do estado da Bahia nos últimos 5 anos.  


## Etapas do projeto:
1. Selecionar a Base de Dados
2. Definir Objetivo e Perguntas
3. Realizar Análise Exploratória
4. Gerar Base Final
5. Criar Visualizações no Tableau
6. Apresentação Final

---

## Bases Escolhidas  

- **Base 1**: [MapBiomas Alertas](https://plataforma.alerta.mapbiomas.org/downloads)

![image](https://github.com/user-attachments/assets/c88130d7-548c-4b12-9af6-8c31a6f222d7)

- **Base 2**: [Sistema de Estimativas de Emissões e Remoções de Gases de Efeito Estufa (SEEG)](https://plataforma.seeg.eco.br/?highlight=states-net-emissions-by-sector-goias&_gl=1*1nqir75*_ga*NTI0MDk2MzUwLjE3Mjc1NDQ0NjA.*_ga_XZWSWEJDWQ*MTcyNzU0NDQ2MC4xLjAuMTcyNzU0NDQ2MC4wLjAuMA..)

![image](https://github.com/user-attachments/assets/485e7e6c-9ebf-418c-8e25-d570c54780e1)


---
 
### Objetivo Geral:

Este projeto tem como objetivo realizar uma análise exploratória dos dados com o objetivo de identificar variáveis de como as taxas de emissão de CO2 foram impactadas pelo desmatamento nos últimos 5 anos e no período da pandemia.


### As perguntas norteadoras deste projeto são:  

1. Qual a taxa de desmatamento nos biomas/municípios da Bahia e como ela evoluiu no período de 2019 a 2022?
2. Qual a taxa de CO2 nos municípios da Bahia e como ela evoluiu no período de 2019 a 2022?
3. Como o desmatamento na Bahia impacta as taxas de emissão de CO₂? Existe uma relação entre as áreas desmatadas e o aumento de CO2?
4. Quais regiões da Bahia apresentam as maiores emissões de carbono derivadas do desmatamento?
5. Houve alguma alteração no período da Pandemia?
---

## Ferramentas Utilizadas  
- **Banco de dados** 
- **Python (Jupyter Notebook)**: Para a análise exploratória de dados utilizando bibliotecas como Pandas, Seaborn, Matplotlib, etc.  
- **Tableau**: Para criar as visualizações finais e apresentar os insights gerados.  
- **GitHub**: Para versionamento do projeto e documentação.  
- **Google Colab**: Para execução de notebooks de forma colaborativa e em nuvem.

---

### Instalações

Instalando o Python: Acesse o site oficial do Python (https://www.python.org/) e baixe a versão mais recente para o seu sistema operacional. Siga as instruções de instalação para configurar o Python em seu computador.

Instalando o Visual Studio Code (VS Code): Acesse o site (https://code.visualstudio.com/).

Extensões que irão tornar o processo de desenvolvimento mais simples e intuitivo:

SQLite: Essa extensão essencial oferece recursos para abrir e editar arquivos SQLite (.db), executar consultas SQL, visualizar dados e até mesmo criar tabelas e colunas diretamente no VS Code.

SQLite Viewer: Com o SQLite Viewer, você pode visualizar seus dados SQLite de forma gráfica, sem precisar escrever código. Ele oferece uma interface simples e amigável para navegar pelas tabelas, visualizar os dados e editar registros.

Bibliotecas e módulos:

sqlite3 csv Pandas Seaborn Matplotlib

---

## Análise exploratória de dados

### 1. DADOS DE CO2 - SEEG

Vamos utilizar a coluna categoria (municipio e total de co2 emitido por tipo de emissão, no caso Mudança de Uso da Terra e Floresta e os anos de 2019 a 2022.

Coleta de dados CO2 Bahia, SEEG:

link: https://plataforma.seeg.eco.br/?highlight=states-net-emissions-by-sector-bahia&_gl=1*gambxz*_ga*MTk5NTgxNjM5MS4xNzI1NjQzNTE1*_ga_XZWSWEJDWQ*MTcyNTY0MzUxNS4xLjAuMTcyNTY0MzUxNS4wLjAuMA..blob:https://plataforma.seeg.eco.br/845fd445-2d02-43a9-bb87-14435bfb6c1b

CO2: quantidade em tonelada

---

```python

# Primeiro, instale a biblioteca pandas se ainda não estiver instalada
!pip install pandas

# Importando os dados
import pandas as pd
import csv

# Carregando os dois arquivos CSV
# Caso esteja rodando localmente, altere o caminho dos arquivos.
# No Colab, você pode fazer upload dos arquivos com os botões de upload e colocar somente o nome do arquivo abaixo

df1 = pd.read_csv('SEEG.csv')
df2 = pd.read_csv('SEEG1.csv')

# Exibindo as primeiras linhas dos DataFrames para verificar
print(df1.head())
print(df2.head())

```


```python

df1.info()
df2.info()

```


```python

# Converta todas as colunas de anos para string, por exemplo

df1[['2019', '2020', '2021', '2022']] = df1[['2019', '2020', '2021', '2022']].astype(float)
df2[['2019', '2020', '2021', '2022']] = df2[['2019', '2020', '2021', '2022']].astype(float)

# Converta a coluna Categoria também, se necessário
df1['Categoria'] = df1['Categoria'].astype(str)
df2['Categoria'] = df2['Categoria'].astype(str)


# Exibindo as primeiras linhas dos DataFrames para verificar
print(df1.head())
print(df2.head())

```


```python

# Remover espaços em branco no início e no fim dos valores das colunas de chave

df1['Categoria'] = df1['Categoria'].str.strip()
df2['Categoria'] = df2['Categoria'].str.strip()



# Exibindo as primeiras linhas dos DataFrames para verificar
print(df1.head())
print(df2.head())

```


```python

print("Valores únicos de Categoria no df1:", df1['Categoria'].unique())
print("Valores únicos de Categoria no df2:", df2['Categoria'].unique())

```


```python

# Fazendo a mesclagem com base em várias colunas
df_merged = pd.merge(df1, df2, on=['Categoria', '2019', '2020', '2021', '2022'], how='outer', suffixes=('.x', '.y'))


# Exibindo as primeiras linhas do arquivo mesclado
print(df_merged.head())


```


```python

df_merged.info()

```

```python

# Exibe os nomes das colunas
df_merged.columns

```


```python

# Selecionar as colunas específicas

df_reduzido = df_merged[['Categoria','2019', '2020', '2021', '2022']]
print(df_reduzido)

```



```python

# Altera os nomes das colunas

df_reduzido.columns = ['Municípios', '2019', '2020', '2021', '2022']
print(df_reduzido)

```


```python

# Verifica valores nulos

nulos = df_reduzido.isnull()
print(nulos)

# Contagem de valores nulos em cada coluna

nulos_por_coluna = df_reduzido.isnull().sum()
print(nulos_por_coluna)

```


```python

# Remove linhas duplicadas

df_sem_duplicatas = df_reduzido.drop_duplicates()
print(df_sem_duplicatas)

```



```python

df_sem_duplicatas = pd.melt(df_sem_duplicatas, id_vars=['Municípios'], value_vars=['2019', '2020', '2021', '2022'], var_name='Ano', value_name='CO2_emitido')

print(df_sem_duplicatas)

```



```python

# Salvando o arquivo final mesclado em um novo CSV

df_sem_duplicatas.to_csv('co2.csv', index=False, encoding='utf-8')

print(df_sem_duplicatas)

```



## 2. DADOS DESMATAMENTO - MAPBIOMAS

```python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

```


```python

# importando dados

df3 = pd.read_csv('mapbiomas_ba.csv')

# Exibindo as primeiras linhas dos DataFrames para verificar

print(df3.head())

```


```python

df3.info()

```



```python

# Converta todas as colunas de anos para int, por exemplo

df3[['ANODETEC']] = df3[['ANODETEC']].astype(int)

df3.info()

```


```python

# Remover múltiplas colunas de uma vez, temos que deixar municipio, area ha (pra calcular o desmatamento, data tec e ano)

colunas_para_remover = ['CODEALERTA', 'FONTE', 'ESTADO', 'DTIMGANT', 'DTIMGDEP', 'DTPUBLI', 'VPRESSAO']

df3_limpo = df3.drop(columns=colunas_para_remover)

print(df3_limpo.head())

```


```python

print(df3_limpo.info())

```


```python

# Verificar se tem valores faltantes

print(df3_limpo.isnull().sum())

```


```python

# Agrupamentos

df3_MUN = df3_limpo.groupby('MUNICIPIO')['AREAHA'].sum().reset_index()

# Mostrar o resultado
print(df3_MUN.head())

df3_ANO = df3_limpo.groupby('ANODETEC')['AREAHA'].sum().reset_index()

# Mostrar o resultado
print(df3_ANO.head())

```


```python

# Salvando o arquivo final em um novo CSV

df3_limpo.to_csv('desmatamento.csv', index=False)

print(df3_limpo)

```
