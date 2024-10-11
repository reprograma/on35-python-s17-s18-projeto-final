# Projeto Final 

Desenvolvido por:

Paloma Avena palomaavena@gmail.com

Anne Ribeiro anne.asribeiro@gmail.com

---

## Contexto

Nos últimos anos, a questão do desmatamento e suas consequências ambientais têm se tornado uma preocupação crescente. A Bahia, por ser um estado de grande diversidade biológica, possui áreas significativas de florestas e biomas que desempenham um papel vital na regulação climática. O desmatamento pode impactar diretamente as emissões de dióxido de carbono (CO₂), contribuindo para o aquecimento global e alterações climáticas.

---
## Etapas do projeto:

Selecionar a Base de Dados
Definir Objetivo e Perguntas
Realizar Análise Exploratória
Gerar Base Final
Criar Visualizações no Tableau
Preparar Apresentação Final

---

## Bases de dados 

- **Base 1**: [MapBiomas Alertas](https://plataforma.alerta.mapbiomas.org/downloads)

- Dados de áreas(ha) desmatada por Municipío, Fator de pressão e Biomas no estado da Bahia.

![image](https://github.com/user-attachments/assets/c88130d7-548c-4b12-9af6-8c31a6f222d7)

- **Base 2**: [Sistema de Estimativas de Emissões e Remoções de Gases de Efeito Estufa (SEEG)](https://plataforma.seeg.eco.br/?highlight=states-net-emissions-by-sector-goias&_gl=1*1nqir75*_ga*NTI0MDk2MzUwLjE3Mjc1NDQ0NjA.*_ga_XZWSWEJDWQ*MTcyNzU0NDQ2MC4xLjAuMTcyNzU0NDQ2MC4wLjAuMA..)
- Dados de CO2 em toneladas por Municípios e Biomas de Mudanças e usos do solo e floresta.

![image](https://github.com/user-attachments/assets/485e7e6c-9ebf-418c-8e25-d570c54780e1)

---
 
### Objetivo Geral:

Este projeto tem como objetivo analisar os dados de desmatamento e emissões de CO₂ no estado da Bahia entre 2019 e 2022, a fim de entender como o desmatamento tem impactado as emissões de carbono no período da Pandemia.

---

### As perguntas norteadoras deste projeto são:  

Como o desmatamento na Bahia impacta as taxas de emissão de CO₂?
Qual a taxa de desmatamento nos municípios e biomas da Bahia entre 2019 e 2022?
Existe uma correlação entre as áreas desmatadas e o aumento das emissões de CO₂?
Como a pandemia afetou as taxas de desmatamento e emissões de CO₂?

---

### Desafios:

Identificar regiões com maior desmatamento e correlacionar com dados de emissões.
Avaliar se as políticas públicas e ações de preservação tiveram impacto nos índices de desmatamento durante o período estudado.
Analisar o efeito da pandemia nas taxas de desmatamento e emissões.
Direcionamentos:

Para abordar esses desafios, criamos uma base de dados unificada com as informações de desmatamento e emissões de CO₂.

Utilizamos técnicas de análise de dados para identificar padrões e correlações entre as variáveis:

Análise temporal: Avaliamos a evolução do desmatamento e das emissões ao longo dos anos, de 2019 a 2022. Os resultados mostram picos em anos específicos, e um declínio temporário durante o período da pandemia, seguido de um aumento substancial em 2021.

Correlações regionais: Mapeamos as emissões de CO₂ e áreas desmatadas por município, identificando as regiões da Bahia mais afetadas. Descobrimos que áreas como o Oeste da Bahia, caracterizadas pelo agronegócio, registram as maiores emissões.

Modelos preditivos: Aplicamos regressão para prever o impacto do aumento do desmatamento nas emissões de CO₂, destacando como a degradação ambiental se traduz diretamente em maiores emissões de gases de efeito estufa.

Impacto da pandemia: Durante a pandemia, observamos uma queda temporária nas emissões devido à redução das atividades econômicas, mas o desmatamento continuou em algumas regiões, mostrando a resiliência desse problema mesmo em crises globais.

## Ferramentas Utilizadas:

Banco de dados Python (Jupyter Notebook): Para a análise exploratória de dados utilizando bibliotecas como Pandas, Seaborn, Matplotlib, etc. Tableau: Para criar as visualizações finais e apresentar os insights gerados. GitHub: Para versionamento do projeto e documentação. Google Colab (opcional): Para execução de notebooks de forma colaborativa e em nuvem.

Instalando o Python: Acesse o site oficial do Python (https://www.python.org/) e baixe a versão mais recente para o seu sistema operacional. Siga as instruções de instalação para configurar o Python em seu computador.

Instalando o Visual Studio Code (VS Code): Acesse o site (https://code.visualstudio.com/).

Extensões que irão tornar o processo de desenvolvimento mais simples e intuitivo:

SQLite: Essa extensão essencial oferece recursos para abrir e editar arquivos SQLite (.db), executar consultas SQL, visualizar dados e até mesmo criar tabelas e colunas diretamente no VS Code.

SQLite Viewer: Com o SQLite Viewer, você pode visualizar seus dados SQLite de forma gráfica, sem precisar escrever código. Ele oferece uma interface simples e amigável para navegar pelas tabelas, visualizar os dados e editar registros.

**Bibliotecas e módulos**:

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

# 1. Importando os dados das planilhas

# Primeiro, instale a biblioteca pandas se ainda não estiver instalada
!pip install pandas

# Importando os dados
import pandas as pd
import csv

# Carregando os dois arquivos CSV
# Caso esteja rodando localmente, altere o caminho dos arquivos, no Colab, você pode fazer upload dos arquivos e colocar o nome do arquivo abaixo:

df1 = pd.read_csv('SEEG.csv')


# Exibindo as primeiras linhas dos DataFrames para verificar
print(df1.head())

```


```python

# 2. Verificar informações gerais dos DataFrames

df1.info()
     

```


```python


# Selecionar as colunas específicas

df_1 = df1[['Categoria','2019', '2020', '2021', '2022']]
print(df_1)

```


```python


# Altera os nomes das colunas

df_1.columns = ['Municípios', '2019', '2020', '2021', '2022']
print(df_1)


```


```python

# Remover informações de estado (como "(BA)") de 'Municípios'

df_1['Municípios'] = df_1['Municípios'].str.replace(r' ', '', regex=True)

print(df_1)


```


```python

df_merged.info()

```

```python

# Converta todas as colunas de anos para inteiro

df_1[['2019', '2020', '2021', '2022']] = df_1[['2019', '2020', '2021', '2022']].astype(int)

print(df_1)

```


```python

# Contagem de valores nulos em cada coluna

nulos_por_coluna1 = df_1.isnull().sum()
print(nulos_por_coluna1)


```


```python

# Remove linhas duplicadas

df_sem_duplicatas1 = df_1.drop_duplicates()
print(df_sem_duplicatas1)

```


```python

# Transformar os dados para um formato longo (melt)

df_sem_duplicatas1 = pd.melt(df_1, id_vars=['Municípios'], value_vars=['2019', '2020', '2021', '2022'], var_name='Ano', value_name='CO2_emitido')

print(df_sem_duplicatas1)


```



```python

# Calcular o total da coluna 'valor'
valor_total = df1['2022'].sum()
print("O valor total da coluna 'valor' é:", valor_total)

```



```python


# Salvando o arquivo final em um novo CSV

df_sem_duplicatas1.to_csv('co2.csv', index=False, encoding='utf-8')

print(df_sem_duplicatas1)


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

# Converta todas as colunas de anos para int

df3[['ANODETEC']] = df3[['ANODETEC']].astype(int)

df3.info()

```


```python

# Remover múltiplas colunas de uma vez, temos que deixar municipio, area ha (pra calcular o desmatamento, data tec e ano)

colunas_para_remover = ['CODEALERTA', 'FONTE', 'DTIMGANT', 'DTIMGDEP', 'DTPUBLI', 'DATADETEC']

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


df3_MUN = df3_limpo.groupby('MUNICIPIO')['AREAHA'].sum().reset_index()

# Mostrar o resultado
print(df3_MUN.head())

df3_ANO = df3_limpo.groupby('ANODETEC')['AREAHA'].sum().reset_index()

# Mostrar o resultado
print(df3_ANO.head())

```

```python

# Salvando o arquivo final em um novo CSV

df3_limpo.to_csv('desmatamento.csv', index=False, encoding='utf-8')

print(df3_limpo)

```


## 3. Integração dos Dados de CO₂ e Desmatamento por Município


``` python

# importando dados

df_desmatamento = pd.read_csv('desmatamento.csv')

df_co2 = pd.read_csv('co2.csv')

# Exibindo as primeiras linhas dos DataFrames para verificar

print(df_desmatamento.head())

print(df_co2.head())

```


```python

# Limpar e padronizar os nomes de municípios

df_desmatamento['MUNICIPIO'] = df_desmatamento['MUNICIPIO'].str.strip().str.lower()
df_co2['Municípios'] = df_co2['Municípios'].str.strip().str.lower()

# Exibindo as primeiras linhas dos DataFrames para verificar

print(df_desmatamento.head())

print(df_co2.head())


```



```python


# Remove linhas duplicadas

df_desmatamentos = df_desmatamento.drop_duplicates()
print(df_desmatamentos)


df_co2s = df_co2.drop_duplicates()
print(df_co2s)

```



```python

# Realizar a junção das tabelas com base nos municípios e anos
df_integrado = pd.merge(df_desmatamentos, df_co2s, left_on=['MUNICIPIO', 'ANODETEC'], right_on=['Municípios', 'Ano'], how='inner')

# Exibir as primeiras linhas da tabela integrada
df_integrado.head()

```



```python


# Verificar se os valores de 'MUNICIPIO' e 'Municípios' são iguais
df_integrado['MUNICIPIO_igual'] = df_integrado['MUNICIPIO'] == df_integrado['Municípios']

# Verificar se os valores de 'ANODETEC' e 'Ano' são iguais
df_integrado['ANODETEC_igual'] = df_integrado['ANODETEC'] == df_integrado['Ano']

# Verificar se há algum False na coluna 'MUNICIPIO_igual'
tem_falso_municipio = df_integrado['MUNICIPIO_igual'].any() == False

# Verificar se há algum False na coluna 'ANODETEC_igual'
tem_falso_ano = df_integrado['ANODETEC_igual'].any() == False

print(f"Tem algum 'False' na comparação de Município? {tem_falso_municipio}")
print(f"Tem algum 'False' na comparação de Ano? {tem_falso_ano}")

```



```python


#Unificando colunas iguais:
df_integrado['MUNICIPIO'] = df_integrado['MUNICIPIO']

df_integrado['ANO'] = df_integrado['Ano']


# Agora podemos excluir as colunas antigas

df_integrado = df_integrado.drop(columns=['Municípios', 'MUNICIPIO_igual'])
df_integrado = df_integrado.drop(columns=['ANODETEC', 'Ano', 'ANODETEC_igual'])

# Exibir as primeiras linhas da tabela integrada
df_integrado.head()

```



```python

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


```



```python


# Definir o estilo para os gráficos
sns.set(style="whitegrid")

```





```python


# 1. Gráfico de barras: Desmatamento total por ano
plt.figure(figsize=(10,6))
sns.barplot(x='ANO', y='AREAHA', data=df_integrado, estimator=sum, ci=None, color='teal')
plt.title('Total de Área Desmatada por Ano (Bahia)', fontsize=14)
plt.xlabel('Ano', fontsize=12)
plt.ylabel('Área Desmatada (ha)', fontsize=12)
plt.xticks(rotation=45)
plt.show()

# 2. Gráfico de barras: Emissões de CO₂ por ano
plt.figure(figsize=(10,6))
sns.barplot(x='ANO', y='CO2_emitido', data=df_integrado, estimator=sum, ci=None, color='orange')
plt.title('Emissões de CO₂ por Ano (Bahia)', fontsize=14)
plt.xlabel('Ano', fontsize=12)
plt.ylabel('Emissões de CO₂ (ton)', fontsize=12)
plt.xticks(rotation=45)
plt.show()

```




```python


# Gráfico de barras empilhadas: Desmatamento e CO₂ emitido nos 10 municípios com mais desmatamento
plt.figure(figsize=(12,7))

# Selecionar os 10 municípios com maiores áreas desmatadas
municipios_mais_desmatados = df_integrado.groupby('MUNICIPIO')['AREAHA'].sum().nlargest(10).index

# Filtrar o DataFrame para incluir apenas os 10 municípios selecionados
df_municipios_desmatados = df_integrado[df_integrado['MUNICIPIO'].isin(municipios_mais_desmatados)]

# Criar gráfico de barras empilhadas com área desmatada e CO₂ emitido
sns.barplot(x='MUNICIPIO', y='CO2_emitido', data=df_municipios_desmatados, hue='ANO', ci=None, palette='viridis')
plt.title('Emissões de CO₂ nos 10 Municípios com Mais Desmatamento por Ano', fontsize=14)
plt.xlabel('Município', fontsize=12)
plt.ylabel('Emissões de CO₂ (ton)', fontsize=12)
plt.xticks(rotation=45)
plt.legend(title='Ano')
plt.show()

```



```python

# Gráfico de barras para Emissões de CO2 por Município

# Ordenar os municípios por CO2_emitido
df_sorted = df.sort_values(by='CO2_emitido', ascending=False)

# Criar gráfico de barras para CO2 emitido por município
plt.figure(figsize=(12,8))
sns.barplot(x='CO2_emitido', y='MUNICIPIO', data=df_sorted, palette='Reds')

plt.title('Emissões de CO2 por Município (Cerrado, Bahia)', fontsize=16)
plt.xlabel('Emissões de CO2 (toneladas)', fontsize=12)
plt.ylabel('Município', fontsize=12)
plt.tight_layout()
plt.show()


# Gráfico de barras para Área Desmatada por Município

# Ordenar os municípios por área desmatada
df_sorted_area = df.sort_values(by='AREAHA', ascending=False)

# Criar gráfico de barras para área desmatada por município
plt.figure(figsize=(12,8))
sns.barplot(x='AREAHA', y='MUNICIPIO', data=df_sorted_area, palette='Greens')

plt.title('Área Desmatada por Município (Cerrado, Bahia)', fontsize=16)
plt.xlabel('Área Desmatada (hectares)', fontsize=12)
plt.ylabel('Município', fontsize=12)
plt.tight_layout()
plt.show()



```



```python

import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

# Criar gráfico de dispersão
plt.figure(figsize=(12, 8))
sns.scatterplot(data=df, x='AREAHA', y='CO2_emitido', color='blue', alpha=0.6)

# Calcular a linha de tendência
x = df['AREAHA']
y = df['CO2_emitido']
m, b = np.polyfit(x, y, 1)  # Ajustar uma linha de tendência (y = mx + b)
plt.plot(x, m*x + b, color='red', linewidth=2, label='Linha de Tendência')

# Adicionar títulos e rótulos
plt.title('Relação entre Área Desmatada e Emissões de CO2', fontsize=16)
plt.xlabel('Área Desmatada (hectares)', fontsize=12)
plt.ylabel('Emissões de CO2 (toneladas)', fontsize=12)
plt.legend()
plt.tight_layout()
plt.show()

```



```python

# Calcular a correlação
correlacao = df['AREAHA'].corr(df['CO2_emitido'])
print(f'A correlação entre a área desmatada e CO2 emitido é: {correlacao}')

# Interpretar a correlação
if correlacao > 0:
    print("Correlação positiva: À medida que a área desmatada aumenta, as emissões de CO2 também tendem a aumentar.")
elif correlacao < 0:
    print("Correlação negativa: À medida que a área desmatada aumenta, as emissões de CO2 tendem a diminuir.")
else:
    print("Sem correlação: Não há relação clara entre as duas variáveis.")


```





```python

# Gráfico de calor: Correlação entre desmatamento e CO₂ emitido
plt.figure(figsize=(8,6))
correlation_matrix = df_integrado[['AREAHA', 'CO2_emitido']].corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', linewidths=0.5)
plt.title('Correlação entre Desmatamento e CO₂ Emitido', fontsize=14)
plt.show()

```




```python

# Gráfico de dispersão: Relação entre área desmatada e CO₂ emitido
plt.figure(figsize=(10,6))
sns.scatterplot(x='AREAHA', y='CO2_emitido', data=df_integrado, hue='ANO', palette='coolwarm', s=100)
plt.title('Relação entre Área Desmatada e CO₂ Emitido', fontsize=14)
plt.xlabel('Área Desmatada (ha)', fontsize=12)
plt.ylabel('CO₂ Emitido (ton)', fontsize=12)
plt.legend(title='Ano')
plt.show()



```




```python


# Gráficos separados: Desmatamento e CO₂ por município para os 10 municípios mais desmatados
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



```python



```






## 5. Banco de dados


```python

import sqlite3
import pandas as pd
from sqlalchemy import create_engine
#from google.colab import files

# Passo 1: Fazer upload do arquivo CSV
# uploaded = files.upload()

# Passo 2: Ler o CSV em um DataFrame
df = pd.read_csv('dados_integrados.csv')

# Passo 3: Criar o engine para o SQLite
engine = create_engine('sqlite:///banco.db')  #abre e fecha conexões

# Passo 4: Inserir o DataFrame no banco de dados SQLite
df.to_sql('desmatamento_co2', con=engine, if_exists='replace', index=False)

print("Dados inseridos com sucesso no SQLite!")

# Passo 5: Consultar o banco de dados
conn = sqlite3.connect('banco.db')
cursor = conn.cursor()

# Fazer uma consulta
cursor.execute("SELECT * FROM desmatamento_co2 LIMIT 5")
rows = cursor.fetchall()

# Mostrar os resultados
for row in rows:
    print(row)

# Fechar a conexão
conn.close()


```


## 6. Considerações

A análise inicial dos dados revelou que, apesar dos esforços de preservação, o desmatamento em várias regiões da Bahia aumentou significativamente nos últimos anos. Isso ocorre especialmente em áreas de biomas sensíveis, como a Caatinga e o Cerrado, que são biomas predominantes no estado.

Esse aumento no desmatamento está intimamente relacionado ao aumento das emissões de CO₂, um dos principais gases responsáveis pelo efeito estufa. O impacto negativo do desmatamento é agravado pelo fato de que essas áreas desmatadas são substituídas por atividades que emitem ainda mais CO₂, como a agropecuária.

Entretanto, as taxas de desmatamento e emissões de CO₂ apresentaram flutuações durante a pandemia de COVID-19, o que levanta questões sobre o papel de eventos globais e econômicos na redução temporária das atividades humanas e como isso afetou o meio ambiente local.

Os resultados da análise reforçam a correlação direta entre desmatamento e emissões de CO₂ no estado da Bahia.

Regiões com maiores áreas desmatadas apresentaram emissões de carbono proporcionalmente mais elevadas, principalmente em áreas destinadas à agropecuária.

A pandemia trouxe uma breve redução nas emissões, mas o desmatamento continuou a crescer, destacando a necessidade de políticas públicas mais robustas e eficientes para combater essa tendência.

A expansão agrícola é um dos principais motores do desmatamento e das emissões de CO₂ na Bahia.

Apesar da breve redução de emissões durante a pandemia, o desmatamento persistiu, o que sugere que fatores locais (como a pressão econômica) têm um papel crucial no aumento da degradação ambiental.

Medidas de mitigação mais efetivas, incluindo a fiscalização e preservação de áreas naturais, são fundamentais para controlar as emissões de carbono derivadas do desmatamento.
