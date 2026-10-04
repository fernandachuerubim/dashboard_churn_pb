# 📊 Dashboard de Clientes de Cartão de Crédito — Power BI

## 📌 Sobre o projeto

Este projeto foi desenvolvido no **Power BI** com o objetivo de analisar o perfil de clientes de cartão de crédito e acompanhar indicadores relacionados à **retenção e churn**.

O dashboard permite explorar características demográficas e comportamentais da base de clientes, facilitando a identificação de padrões entre clientes ativos e clientes que encerraram o relacionamento.

---

## 🎯 Objetivos

- Monitorar o número total de clientes.
- Acompanhar clientes existentes e clientes em churn.
- Comparar o perfil de clientes por gênero.
- Analisar distribuição por nível educacional.
- Avaliar clientes por faixa de renda.
- Analisar estado civil.
- Comparar categorias de cartão.
- Avaliar a distribuição dos clientes por faixa etária.
- Permitir análises dinâmicas através de filtros.

---

## 📊 Principais indicadores

O dashboard apresenta os seguintes KPIs:

- **Clientes:** total de clientes da base.
- **Clientes Churn:** clientes classificados como `Attrited Customer`.
- **Clientes Existentes:** clientes classificados como `Existing Customer`.

Os indicadores são dinâmicos e respondem aos filtros aplicados no relatório.

---

## 📈 Visualizações do dashboard

O relatório contém análises de:

- **Gênero**
- **Gênero x Nível Educacional**
- **Faixa de Renda**
- **Gênero x Estado Civil**
- **Gênero x Categoria de Cartão**
- **Faixa Etária x Gênero**

Também foi utilizado um filtro de **Attrition Flag**, permitindo selecionar:

- `Existing Customer`
- `Attrited Customer`

Dessa forma, todas as visualizações podem ser analisadas de acordo com a situação atual do cliente.

---

## 👥 Faixas etárias

Para facilitar a análise, os clientes entre 26 e 58 anos foram agrupados em cinco faixas:

| Faixa |
|---|
| 26–32 anos |
| 33–39 anos |
| 40–46 anos |
| 47–52 anos |
| 53–58 anos |

Exemplo da coluna calculada utilizada:

```DAX
Faixa_Idade =
SWITCH(
    TRUE(),
    BankChurners[Customer_Age] >= 26 && BankChurners[Customer_Age] <= 32, "26-32",
    BankChurners[Customer_Age] >= 33 && BankChurners[Customer_Age] <= 39, "33-39",
    BankChurners[Customer_Age] >= 40 && BankChurners[Customer_Age] <= 46, "40-46",
    BankChurners[Customer_Age] >= 47 && BankChurners[Customer_Age] <= 52, "47-52",
    BankChurners[Customer_Age] >= 53 && BankChurners[Customer_Age] <= 58, "53-58",
    BLANK()
)
```

---

## 🧮 Medidas DAX

### Total de clientes

```DAX
Clientes =
COUNTROWS(BankChurners)
```

Essa medida permite que o total seja atualizado automaticamente conforme os filtros aplicados no dashboard.

### Clientes existentes

```DAX
Existing_Customers =
CALCULATE(
    COUNTROWS(BankChurners),
    KEEPFILTERS(
        BankChurners[Attrition_Flag] = "Existing Customer"
    )
)
```

### Clientes em churn

```DAX
Attrited_Customers =
CALCULATE(
    COUNTROWS(BankChurners),
    KEEPFILTERS(
        BankChurners[Attrition_Flag] = "Attrited Customer"
    )
)
```

---

## 🛠️ Tecnologias utilizadas

- **Power BI**
- **Power Query**
- **DAX**
- **Modelagem de Dados**
- **Visualização de Dados**
- **Análise Exploratória de Dados**

---

## 💡 Competências demonstradas

Este projeto demonstra conhecimentos em:

- Criação de dashboards interativos.
- Construção de KPIs.
- Criação de medidas e colunas calculadas em DAX.
- Segmentação e categorização de dados.
- Aplicação de filtros dinâmicos.
- Análise de churn.
- Construção de visualizações voltadas para tomada de decisão.
- Organização visual de relatórios gerenciais.

---

## 🔎 Possíveis análises

Com o dashboard é possível responder perguntas como:

- Em quais faixas etárias existe maior concentração de clientes?
- Existe diferença de churn entre homens e mulheres?
- Quais faixas de renda possuem mais clientes?
- Qual categoria de cartão concentra a maior quantidade de clientes?
- Como o nível educacional se distribui entre os gêneros?
- Qual é o perfil demográfico predominante da base?

---

## 📂 Estrutura sugerida do repositório

```text
power-bi-credit-card-dashboard/
│
├── README.md
├── dashboard.pbix
└── data/
    └── BankChurners.csv
```

---

## 🚀 Como utilizar

1. Faça o download do arquivo `.pbix`.
2. Abra o projeto no **Power BI Desktop**.
3. Atualize a fonte de dados, caso necessário.
4. Utilize o filtro **Attrition Flag** para alternar entre clientes existentes e clientes em churn.
5. Explore os demais gráficos para analisar o perfil da base de clientes.

---

## 📌 Contexto do projeto

Projeto desenvolvido para fins de **estudo e portfólio em análise de dados / Business Intelligence**, com foco na construção de um dashboard de clientes de cartão de crédito e análise de churn com uso de Power BI e com uso de banco de dados público do KAGGLE.

---


