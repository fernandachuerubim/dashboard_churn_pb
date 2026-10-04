# credit_customer_pb

Projeto **Power BI** (formato `.pbip` — Power BI Project) para análise de **churn de clientes de cartão de crédito**, construído sobre o dataset público **BankChurners**. O projeto contém um modelo semântico em TMDL e um relatório com uma página de dashboard.

---

## Estrutura do projeto

```
credit_customer_pb/
├── credit_customer.pbip                  # Arquivo de projeto Power BI (entry point)
├── credit_customer.pbix                  # Binário do Power BI Desktop
├── credit_customer.SemanticModel/        # Modelo semântico (TMDL)
│   ├── definition.pbism
│   ├── diagramLayout.json                # Layout do diagrama ("Todas as tabelas")
│   ├── .platform                         # Metadados Fabric (SemanticModel: credit_customer)
│   ├── .pbi/                             # Configurações locais, editor e cache
│   └── definition/
│       ├── model.tmdl                    # Definição do modelo (culture: pt-BR)
│       ├── database.tmdl                 # compatibilityLevel: 1606
│       ├── tables/BankChurners.tmdl      # Única tabela do modelo
│       └── cultures/pt-BR.tmdl           # Metadados linguísticos (pt-BR)
└── credit_customer.Report/               # Relatório
    ├── definition.pbir                   # Referência: ../credit_customer.SemanticModel
    ├── .platform                         # Metadados Fabric (Report: credit_customer)
    ├── .pbi/
    ├── StaticResources/.../Fluent2-CY26SU09.json   # Tema Fluent 2
    └── definition/
        ├── report.json / version.json    # version: 2.0.0
        └── pages/ffa9fa2325de6b9b9ad8/ # Página "Dashboard" (1920×1080)
```

### Tabela `BankChurners`

**Colunas de fonte (21):**

| Coluna | Tipo | Descrição |
|---|---|---|
| `CLIENTNUM` | int64 | Identificador do cliente |
| `Attrition_Flag` | string | "Existing Customer" / "Attrited Customer" |
| `Customer_Age` | int64 | Idade do cliente |
| `Gender` | string | Gênero |
| `Dependent_count` | int64 | Número de dependentes |
| `Education_Level` | string | Escolaridade |
| `Marital_Status` | string | Estado civil |
| `Income_Category` | string | Faixa de renda |
| `Card_Category` | string | Categoria do cartão (Blue/Silver/Gold/Platinum) |
| `Months_on_book` | int64 | Meses como cliente |
| `Total_Relationship_Count` | int64 | Total de produtos/relacionamentos |
| `Months_Inactive_12_mon` | int64 | Meses inativo (últimos 12 meses) |
| `Contacts_Count_12_mon` | int64 | Contatos (últimos 12 meses) |
| `Credit_Limit` | int64 | Limite de crédito |
| `Total_Revolving_Bal` | int64 | Saldo rotativo total |
| `Avg_Open_To_Buy` | int64 | Média de limite disponível |
| `Total_Amt_Chng_Q4_Q1` | int64 | Variação de valor transacionado Q4/Q1 |
| `Total_Trans_Amt` | int64 | Valor total de transações |
| `Total_Trans_Ct` | int64 | Quantidade de transações |
| `Total_Ct_Chng_Q4_Q1` | int64 | Variação de contagem Q4/Q1 |
| `Avg_Utilization_Ratio` | int64 | Taxa média de utilização |

**Coluna calculada:**

- `Faixa_Idade` — segmenta `Customer_Age` em faixas: `26-32`, `33-39`, `40-46`, `47-52`, `53-58` (fora dessas faixas retorna `BLANK()`), implementada com `SWITCH(TRUE(), ...)`.

**Medidas:**

| Medida | Definição |
|---|---|
| `Existing_Customers` | `CALCULATE(COUNTROWS(BankChurners), KEEPFILTERS(Attrition_Flag = "Existing Customer"))` |
| `Attrited_Customers` | `CALCULATE(COUNTROWS(BankChurners), KEEPFILTERS(Attrition_Flag = "Attrited Customer"))` |

Ambas com `formatString: 0`.

---

## Relatório — Dashboard

Página única **"Dashboard"** (1920×1080, `FitToPage`), título "DASHBOARD DE CLIENTES DE CARTÃO DE CRÉDITO" (bold, 28pt, centralizado), tema **Fluent 2**.

**12 visuais:**

| Tipo | Campos | Posição (x, y) |
|---|---|---|
| Card (KPI) | `CLIENTNUM` (contagem — total de clientes) | 26, 92 |
| Card (KPI) | `Attrited_Customers` | 246, 90 |
| Card (KPI) | `Existing_Customers` | 506, 90 |
| Slicer | `Attrition_Flag` | 830, 92 |
| Pizza | `Gender` | 26, 204 |
| Colunas agrupadas | `Education_Level` × `Gender` | 609, 204 |
| Barras agrupadas | `Income_Category` × `Gender` | 1188, 204 |
| Colunas agrupadas | `Marital_Status` × `Gender` | 26, 596 |
| Colunas agrupadas | `Card_Category` × `Gender` | 622, 596 |
| Barras agrupadas | `Faixa_Idade` | 1186, 596 |

Os gráficos usam `Gender` como série (comparação masculino/feminino) e agregação de contagem.

---

## Licença / origem dos dados

Dataset **BankChurners** (dataset público de churn de clientes de cartão de crédito, com scores de classificadores Naive Bayes — colunas removidas na modelagem).
