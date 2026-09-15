# ENG4402-Trabalho-Eng-de-dados

Projeto de modelagem relacional e ETL sobre educação básica brasileira, cruzando três fontes do INEP/MEC: **Censo Escolar**, **IDEB** e **INSE** (ano de referência: 2023).

## 📁 Estrutura do repositório

```
Data/
├── Censo/
│   ├── dados/                         ← CSV bruto (não versionado, ver "Dados brutos" abaixo)
│   ├── Anexos/                        ← dicionário de dados e questionários (versionado)
│   └── leia-me/                       ← notas de uso do INEP (versionado)
├── INDEB/
│   ├── divulgacao_anos_iniciais_escolas_2025/   ← xlsx bruto (não versionado)
│   ├── divulgacao_anos_finais_escolas_2025/     ← xlsx bruto (não versionado)
│   └── divulgacao_ensino_medio_escolas_2025/    ← xlsx bruto (não versionado)
├── INSE/
│   ├── INSE_2023_escolas.xlsx         ← bruto (não versionado)
│   └── INSE_2023_escolas.csv          ← conversão direta do xlsx, sem tratamento
└── processed/                         ← ✅ dados já limpos, versionados neste repositório
    ├── censo_escolar_2023_tratado.csv
    ├── censo_escolar_2023_tratado.parquet
    ├── ideb_ensino_medio_2023_tratado.csv
    └── ideb_ensino_medio_2023_tratado.parquet
```

## ✅ Dados já tratados (estão neste repositório, não precisa baixar nada)

A pasta `Data/processed/` já vem com os arquivos prontos, com colunas reduzidas ao escopo do trabalho (identificação, infraestrutura, matrículas/docentes/turmas do Ensino Médio) e tipos numéricos corrigidos:

| Arquivo | Descrição |
|---|---|
| `censo_escolar_2023_tratado.csv` / `.parquet` | Censo Escolar 2023, reduzido a 35 colunas relevantes ao objetivo do trabalho |
| `ideb_ensino_medio_2023_tratado.csv` / `.parquet` | IDEB do Ensino Médio 2023, só colunas de identificação + indicadores de 2023 |

Basta clonar o repositório e usar direto:

```python
import pandas as pd
df_censo = pd.read_csv("Data/processed/censo_escolar_2023_tratado.csv", sep=";", encoding="utf-8")
df_ideb = pd.read_csv("Data/processed/ideb_ensino_medio_2023_tratado.csv", sep=";", encoding="utf-8")
```

> O arquivo do **INSE** ainda não passou pela etapa de redução/tratamento de colunas — está disponível em `Data/INSE/INSE_2023_escolas.csv` (conversão direta do xlsx original, sem alterações).

## 📥 Dados brutos (originais, sem nenhum tratamento)

Os arquivos **brutos** de Censo Escolar e IDEB não estão versionados no repositório (o CSV do Censo sozinho tem ~200 MB, acima do limite de 100 MB do GitHub). Para obtê-los, baixe diretamente das fontes oficiais:

| Fonte | Link |
|---|---|
| Censo Escolar da Educação Básica 2023 | https://dados.gov.br/dados/conjuntos-dados/inep-microdados-do-censo-escolar-da-educacao-basica |
| IDEB (Escolas → 2023) | https://dados.gov.br/dados/conjuntos-dados/inep-indicador-educacional-da-educacao-basica-indice-de-desenvolvimento-da-educacao-basica-ideb |
| INSE (Escolas → 2023) | https://dados.gov.br/dados/conjuntos-dados/inep-indicador-de-nivel-socioeconomico-inse |

Depois de baixados, coloque cada arquivo na pasta correspondente indicada na estrutura acima (`Data/Censo/dados/`, `Data/INDEB/.../`), respeitando os nomes de arquivo originais — essas pastas já estão no `.gitignore`, então não serão versionadas de novo.

## 🗂 Documentação de apoio (já vem no repositório)

- `Data/Censo/Anexos/ANEXO I - Dicionário de Dados/` — dicionário de colunas do Censo Escolar
- `Data/Censo/Anexos/ANEXO II - Questionários do Censo da Educação Básica/` — PDFs dos formulários (Aluno, Escola, Gestor Escolar, Profissional Escolar, Turma)
- `Data/Censo/leia-me/Leia-me.pdf` — notas de uso do Censo Escolar
- Aba **"Dicionário"** dentro do `INSE_2023_escolas.xlsx` — explica as colunas do INSE

## 🔑 Chaves de cruzamento entre as bases

| Base | Coluna-chave (Código INEP da escola) |
|---|---|
| Censo Escolar | `CO_ENTIDADE` |
| IDEB | `ID_ESCOLA` |
| INSE | `ID_ESCOLA` |

As três bases usam o mesmo identificador de escola, só com nomes de coluna diferentes — é necessário padronizar esse nome durante o ETL antes de cruzar as tabelas.

## 📚 Fontes originais (para referência/citação)

- Censo Escolar: https://dados.gov.br/dados/conjuntos-dados/inep-microdados-do-censo-escolar-da-educacao-basica
- IDEB: https://dados.gov.br/dados/conjuntos-dados/inep-indicador-educacional-da-educacao-basica-indice-de-desenvolvimento-da-educacao-basica-ideb
- INSE: https://dados.gov.br/dados/conjuntos-dados/inep-indicador-de-nivel-socioeconomico-inse

Dados baixados originalmente em: **15/09/2025**.
