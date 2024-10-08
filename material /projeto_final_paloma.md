# Projeto Final de Análise de Dados


**Impacto do Desmatamento e Emissões de CO₂ na Bahia: Uma Análise ambiental no período da Pandemia**

Desenvolvido por:

Paloma Avena palomaavena@gmail.com

Anne Ribeiro anne.asribeiro@gmail.com

## Contexto  

Este projeto tem como foco a criação de um banco de dados e a análise de dados sobre desmatamento e emissões de CO₂ no estado da Bahia nos últimos 5 anos. A partir disso, busca-se entender a relação entre o desmatamento e as emissões de CO₂, analisando possíveis impactos durante o período da pandemia.


## Etapas do projeto:

1.Seleção das Bases de Dados
2.Definição de Objetivo e Perguntas
3.Análise Exploratória
4.Geração da Base Final
5.Criação de Visualizações no Tableau
6.Apresentação Final

---

## Bases Escolhidas  

- **Base 1**: [MapBiomas Alertas](https://plataforma.alerta.mapbiomas.org/downloads)

![image](https://github.com/user-attachments/assets/c88130d7-548c-4b12-9af6-8c31a6f222d7)

- **Base 2**: [Sistema de Estimativas de Emissões e Remoções de Gases de Efeito Estufa (SEEG)](https://plataforma.seeg.eco.br/?highlight=states-net-emissions-by-sector-goias&_gl=1*1nqir75*_ga*NTI0MDk2MzUwLjE3Mjc1NDQ0NjA.*_ga_XZWSWEJDWQ*MTcyNzU0NDQ2MC4xLjAuMTcyNzU0NDQ2MC4wLjAuMA..)

![image](https://github.com/user-attachments/assets/485e7e6c-9ebf-418c-8e25-d570c54780e1)


---
 
### Objetivo Geral:

Realizar uma análise exploratória para identificar como as taxas de emissão de CO₂ foram impactadas pelo desmatamento nos últimos cinco anos, com um olhar específico sobre o período da pandemia.

### As perguntas norteadoras deste projeto são:  

1. Qual foi a taxa de desmatamento nos biomas/municípios da Bahia de 2019 a 2022?
2. Qual foi a taxa de emissões de CO₂ nos municípios da Bahia nesse mesmo período?
3. Qual a relação entre desmatamento e as emissões de CO₂ na Bahia?
4. Quais regiões apresentaram as maiores emissões de CO₂ ligadas ao desmatamento?
5. Houve alguma mudança significativa durante o período da pandemia?
---

## Ferramentas Utilizadas  

- **Banco de dados** 
- **Python (Jupyter Notebook)**: Para a análise exploratória de dados utilizando bibliotecas como Pandas, Seaborn, Matplotlib, etc.  
- **Tableau**: Para criar as visualizações finais e apresentar os insights gerados.  
- **GitHub**: Para versionamento do projeto e documentação.  
- **Google Colab**: Para execução de notebooks de forma colaborativa e em nuvem.

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

# Verificar informações gerais dos DataFrames

df1.info()
df2.info()

```


```python

# Converter todas as colunas de anos para string, por exemplo

df1[['2019', '2020', '2021', '2022']] = df1[['2019', '2020', '2021', '2022']].astype(float)
df2[['2019', '2020', '2021', '2022']] = df2[['2019', '2020', '2021', '2022']].astype(float)

# Remover espaços em branco no início e no fim dos valores das colunas de chave

df1['Categoria'] = df1['Categoria'].str.strip()
df2['Categoria'] = df2['Categoria'].str.strip()


# Exibindo as primeiras linhas dos DataFrames para verificar
print(df1.head())
print(df2.head())

```


```python

# Mesclar os dois DataFrames com base na Categoria e anos
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

# Selecionar colunas relevantes e renomeá-las

df_reduzido = df_merged[['Categoria', '2019', '2020', '2021', '2022']].copy()

# Altera os nomes das colunas

df_reduzido.columns = ['Municípios', '2019', '2020', '2021', '2022']

# Exibir o DataFrame reduzido
print(df_reduzido.head())

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

# Transformar os dados para um formato longo (melt)

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

# Verificar se tem valores nulo

print(df3_limpo.isnull().sum())

```


```python

# Agrupamentos


# Agrupando os dados por município e ano para obter a área desmatada total

df3_final = df3_limpo.groupby(['MUNICIPIO', 'ANODETEC'])['AREAHA'].sum().reset_index()


# Salvando o resultado em CSV
df3_final.to_csv('desmatamento.csv', index=False)

print(df3_final.head())

```


## 3. Integração dos Dados de CO₂ e Desmatamento por Município


``` python

# Limpar e padronizar os nomes de municípios e anos
df_desmatamento['MUNICIPIO'] = df_desmatamento['MUNICIPIO'].str.strip().str.lower()
df_co2['Municípios'] = df_co2['Municípios'].str.strip().str.lower()

# Remover informações de estado (como "(BA)") de 'Municípios'
df_co2['Municípios'] = df_co2['Municípios'].str.replace(r' \(.*\)', '', regex=True)

# Converter as colunas de ano para o mesmo tipo
df_desmatamento['ANODETEC'] = df_desmatamento['ANODETEC'].astype(int)
df_co2['Ano'] = df_co2['Ano'].astype(int)

# Realizar a junção das tabelas com base nos municípios e anos
df_integrado = pd.merge(df_desmatamento, df_co2, left_on=['MUNICIPIO', 'ANODETEC'], right_on=['Municípios', 'Ano'], how='inner')

# Exibir as primeiras linhas da tabela integrada
df_integrado.head()

# Salvando o arquivo final em CSV
df_integrado.to_csv('dados_integrados.csv', index=False, encoding='utf-8')

```

## 4. Visualização

```python

# Importar bibliotecas necessárias
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Carregar os dados integrados
df_integrado = pd.read_csv('dados_integrados.csv')

# Exibir as primeiras linhas do DataFrame para verificar se os dados foram carregados corretamente
print(df_integrado.head())

# Definir o estilo para os gráficos
sns.set(style="whitegrid")

# 1. Gráfico de barras: Desmatamento total por ano
plt.figure(figsize=(10,6))
sns.barplot(x='ANODETEC', y='AREAHA', data=df_integrado, estimator=sum, ci=None, color='teal')
plt.title('Total de Área Desmatada por Ano (Bahia)', fontsize=14)
plt.xlabel('Ano', fontsize=12)
plt.ylabel('Área Desmatada (ha)', fontsize=12)
plt.xticks(rotation=45)
plt.show()

# 2. Gráfico de linha: Emissões de CO₂ por ano
plt.figure(figsize=(10,6))
sns.lineplot(x='Ano', y='CO2_emitido', data=df_integrado, marker='o', color='orange')
plt.title('Emissões de CO₂ por Ano (Bahia)', fontsize=14)
plt.xlabel('Ano', fontsize=12)
plt.ylabel('Emissões de CO₂ (ton)', fontsize=12)
plt.xticks(rotation=45)
plt.show()

# 3. Gráfico de dispersão: Relação entre área desmatada e CO₂ emitido
plt.figure(figsize=(10,6))
sns.scatterplot(x='AREAHA', y='CO2_emitido', data=df_integrado, hue='Ano', palette='coolwarm', s=100)
plt.title('Relação entre Área Desmatada e CO₂ Emitido', fontsize=14)
plt.xlabel('Área Desmatada (ha)', fontsize=12)
plt.ylabel('CO₂ Emitido (ton)', fontsize=12)
plt.legend(title='Ano')
plt.show()

# 4. Gráfico de barras empilhadas: Desmatamento e CO₂ emitido nos 10 municípios com mais desmatamento
plt.figure(figsize=(12,7))

# Selecionar os 10 municípios com maiores áreas desmatadas
municipios_mais_desmatados = df_integrado.groupby('MUNICIPIO')['AREAHA'].sum().nlargest(10).index

# Filtrar o DataFrame para incluir apenas os 10 municípios selecionados
df_municipios_desmatados = df_integrado[df_integrado['MUNICIPIO'].isin(municipios_mais_desmatados)]

# Criar gráfico de barras empilhadas com área desmatada e CO₂ emitido
sns.barplot(x='MUNICIPIO', y='CO2_emitido', data=df_municipios_desmatados, hue='ANODETEC', ci=None, palette='viridis')
plt.title('Emissões de CO₂ nos 10 Municípios com Mais Desmatamento por Ano', fontsize=14)
plt.xlabel('Município', fontsize=12)
plt.ylabel('Emissões de CO₂ (ton)', fontsize=12)
plt.xticks(rotation=45)
plt.legend(title='Ano')
plt.show()

# 5. Gráfico de calor: Correlação entre desmatamento e CO₂ emitido
plt.figure(figsize=(8,6))
correlation_matrix = df_integrado[['AREAHA', 'CO2_emitido']].corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', linewidths=0.5)
plt.title('Correlação entre Desmatamento e CO₂ Emitido', fontsize=14)
plt.show()

# 6. Gráficos separados: Desmatamento e CO₂ por município para os 10 municípios mais desmatados
fig, axs = plt.subplots(2, 1, figsize=(12, 10))

# Gráfico de barras para desmatamento nos 10 municípios mais desmatados
sns.barplot(x='MUNICIPIO', y='AREAHA', data=df_municipios_desmatados, estimator=sum, ci=None, ax=axs[0], color='teal')
axs[0].set_title('Área Desmatada nos 10 Municípios (Bahia)', fontsize=14)
axs[0].set_xlabel('Município', fontsize=12)
axs[0].set_ylabel('Área Desmatada (ha)', fontsize=12)
axs[0].set_xticklabels(axs[0].get_xticklabels(), rotation=45)

# Gráfico de barras para CO₂ nos 10 municípios mais desmatados
sns.barplot(x='MUNICIPIO', y='CO2_emitido', data=df_municipios_desmatados, estimator=sum, ci=None, ax=axs[1], color='orange')
axs[1].set_title('Emissões de CO₂ nos 10 Municípios (Bahia)', fontsize=14)
axs[1].set_xlabel('Município', fontsize=12)
axs[1].set_ylabel('Emissões de CO₂ (ton)', fontsize=12)
axs[1].set_xticklabels(axs[1].get_xticklabels(), rotation=45)

plt.tight_layout()
plt.show()

```

## 5. Banco de dados


## 6. Considerações

Correlações:
Área Desmatada (AREAHHA): 1 (correlação perfeita consigo mesma).
CO₂ Emitido (CO₂_emitido): 1 (correlação perfeita consigo mesma).
Correlação entre Área Desmatada e CO₂ Emitido: 0.19.

A correlação 1 indica uma correlação positiva perfeita (quando uma variável aumenta, a outra também aumenta).
A correlação -1 indica uma correlação negativa perfeita (quando uma variável aumenta, a outra diminui).
0 indica nenhuma correlação.
0.19 é uma correlação fraca e positiva:

Significa que, em geral, há uma leve tendência de que, à medida que a área desmatada aumenta, as emissões de CO₂ também aumentam. No entanto, a correlação é fraca, o que significa que essa relação não é forte ou confiável. Ou seja há uma correlação positiva fraca entre desmatamento e CO₂ emitido, mas ela não é forte o suficiente para concluir que um aumento no desmatamento leva a um aumento significativo nas emissões de CO₂. Uma correlação fraca indica que outros fatores podem estar influenciando as emissões de CO₂ (ou consumo de CO2), e mais análises seriam necessárias para entender essa dinâmica.


Conclusão

Como há uma relação fraca, não podemos afirmar que existe uma correlação forte ou direta entre desmatamento e CO₂ emitido com base nos dados apresentados no éríodo analisado. Isso significa que, enquanto algumas áreas desmatadas podem contribuir para emissões de CO₂, a relação não é consistente o suficiente para prever as emissões apenas com base na área desmatada.
