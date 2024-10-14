## 📝 Contexto
Este projeto consiste na análise de dados de incidentes de violência contra mulheres registrados na cidade de Vila Velha, no estado do Espírito Santo entre os anos de 2022 e 2023.  

## 🎯 Etapas do projeto:
1. **Selecionar a Base de Dados** [Escolher e explorar a base de dados relevante ao tema.] ✅
2. **Definir Objetivo e Perguntas**  [Estabelecer o objetivo e formular perguntas-chave com base nas variáveis disponíveis.] ✅
3. **Realizar Análise Exploratória**  [Identificar correlações, padrões e outliers nos dados.] ✅
4. **Gerar Base Final**  [Limpar e estruturar os dados para a visualização.] ✅
5. **Criar Visualizações no Tableau**  [Desenvolver gráficos que sintetizem os principais insights.] ✅
6. **Preparar Apresentação Final**  [Apresentar o tema, dados e visualizações de forma clara e objetiva.] ✅

---

## 🔗 Base Escolhida
- **Base**: Nome da Base de Dados: Violencia Contra Mulher 2022_2023

Fonte: Dados abertos do estado do Espírito Santo, em que a fonte foi o Observatório Estadual de Segurança Pública. 
Os dados estão disponíveis por meio deste link: https://dados.es.gov.br/dataset/violencia-contra-mulher-2022_2023

---
 
### 💡 Objetivo Geral:
O objetivo deste projeto é analisar os incidentes de violência contra mulheres na cidade de Vila Velha, no estado do Espírito Santo entre os dados de 2022 e 2023. 

O projeto pretende fornecer informações relevantes que promovam a conscientização sobre a violência de gênero, incentivando uma profunda reflexão sobre os desafios enfrentados por mullheres, e sua luta por segurança.

### As perguntas norteadoras deste projeto são:

1. **[Pergunta sobre o perfil dos dados]** - Quais são as principais características da base de dados selecionada? 

A base de dados tem 69.643 linhas e 15 colunas.

As informações são de:

📅 Data do Fato: Data em que o incidente foi registrado.

⏰ Hora do Fato: Hora em que o incidente ocorreu.

📝 Tipo de Boletim: Tipo de boletim de ocorrência registrado.

👤 Tipo de Envolvimento: Indica o tipo de envolvimento da vítima.

🪪 Idade: Idade da vítima.

♀️ Sexo: Sexo da vítima.

✋🏻✋🏽✋🏾 Raça: Raça da vítima.

🔢 Cód. Incidente: Código numérico que classifica o tipo específico do incidente.

📂 Grupo de Incidente: Grupo ao qual o tipo de incidente pertence.

🏷️ Tipo de Incidente: Tipo detalhado de incidente ocorrido.

🗺️ UF: Estado onde o incidente foi registrado.

🏙️ Município: Nome do município onde o incidente ocorreu.

📍 Bairro: Nome do bairro onde o incidente ocorreu.

🏠 Tipo de Local: Tipo de ambiente onde ocorreu o incidente.

Outras características:

- Temporalidade: A base contém dados de 2022 e 2023, abrangendo o período de 2 anos, permitindo a análise de tendências e padrões ao longo do tempo.

- Horário dos crimes: A inclusão de dados sobre a hora do fato possibilita a nálise de padrões temporais, ajudando a identificar por exemplo se certos tipos de violência ocorrem com mais frequência em horários específicos.

- Classificação das violências: A base de dados tem colunas que categorizam os tipos de crimes, como: tipo de boletim, grupo de incidente e tipo de local.

- Variáveis demográficas: A base tem informações sobre as vítimas, como idade, gênero e raça. O que permite uma análise aprofundada das características vas vítimas de violência.

- Geolocalização: Os dados são segmentados por município e bairro, possibilitando uma análise geográfica detalhada e a identificação de áreas com maior incidência de violência.

2. **[Pergunta descritiva]** - Qual é o número total de incidentes de violência contra mulheres registrados em cada bairro de Vila Velha durante os anos de 2022 e 2023?

3. **[Pergunta descritiva]** - Qual é a quantidade de incidentes de violência contra mulheres em Vila Velha, categorizados por tipo de local?  

4. **[Pergunta descritiva]** - Como estão distribuídos os incidentes de violência contra mulheres em Vila Velha, classificados por código e tipo de incidente, nos anos de 2022 e 2023?

5. **[Pergunta descritiva]** - Qual é a distribuição de vítimas de violência contra mulheres em Vila Velha por faixa etária e tipo de incidente registrados em 2022 e 2023?

6. **[Pergunta descritiva]** - Como se distribuem as vítimas de violência contra mulheres em Vila Velha por raça e tipo de incidente, de acordo com os dados de 2022 e 2023?

7. **[Pergunta descritiva]** - Qual é a quantidade de vítimas de violência contra mulheres em Vila Velha, distribuídas por gênero e tipo de incidente, nos anos de 2022 e 2023?

---

## 🛠️ Ferramentas Utilizadas  
- **🐍 Python (Jupyter Notebook)**: Para a análise exploratória de dados utilizando bibliotecas como Pandas, Seaborn, Matplotlib, etc.  
- **📈 Tableau**: Para criar as visualizações finais e apresentar os insights gerados.  
- **💻 GitHub**: Para versionamento do projeto e documentação.  
- **📓 Google Colab** (opcional): Para execução de notebooks de forma colaborativa e em nuvem.  

---

## 💜 Nome do Projeto
Violência contra Mulheres: Estudo de Vila Velha, Espírito Santo.

---

## 🗃️ Organização do Repositório

**Estrutura de Pastas e Arquivos**

### Pasta: `base_de_dados`
- **Arquivo:** `violencia_contra_mulher_2022_2023.csv`
  - Base de dados utilizada para o projeto.

### Pasta: `analise_exploratoria`
- **Arquivo:** `analise_exploratoria.ipynb`
  - Notebook com a análise exploratória, incluindo limpeza, tratamento dos dados e as análises.

### Pasta: `base_final`
- **Arquivo:** `base_final_violencia_contra_mulher_2022_2023.csv`
  - Base final exportada em CSV.

### Pasta: `documentacao_do_projeto`
- **Arquivo:** `violencia_es.md`
  - Arquivo em Markdown com a documentação do projeto.

### Pasta: `analises_no_tableau`
  - **Arquivos:** `1. Bairros com mais indicentes.png`, `2. 10 Bairros com mais incidentes.png`, `3. Incidentes por tipo de local.png`, `4. Locais com mais incidentes.png`, `5. Distribuição dos incidentes.png`, `6. 10 maiores incidentes.png`, `7. Vítimas por idade.png`, `8. Vítimas idade (20 a 45 anos).png`, `9. Vítimas por raça.png`

    - Imagens de gráficos realizados no Tableau.  
 

- **Arquivos:** `10. Dashboard de Visão Geral de Violência Contra Mulheres.png`, `11. Dashboard de Análise de Incidentes de Violência Contra Mulhereres.png`, `12. Dashboard de Perfil das Vítimas de Violência Contra Mulheres.png`
  - Imagens de dashboards realizados no Tableau.

- **Arquivo:** `13. Entendendo os Dados Violência Contra Mulheres.png`
  - Imagem do storytelling realizado no Tableau.

- **Arquivo:**: `analises_no_tableau.md`
  - Arquivo em Markdown com o link do Tableau, com as análises feitas com os gráficos, dashboards e storytelling.

### Pasta: `apresentacao_em_slides`
  - **Arquivo:** `Violência contra Mulheres - Estudo de Vila Velha, Espírito Santo - Sueide Vilela.pdf`
    - Arquivo em PDF com os slides de apresentação do projeto.

---

## 🙋‍♀️ Sobre mim
**Sueide Vilela**

👩‍🎓 Aluna da Turma ON 35 - Análise de Dados com Python

💻 Github: github.com/sueidevilela

🤝 LinkedIn: linkedin.com/in/sueide-vilela

📧 E-mail: sueide.t@gmail.com