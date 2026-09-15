# ENG4402-Trabalho-Eng-de-dados

Projeto de modelagem relacional e ETL sobre educação básica brasileira, cruzando três fontes do INEP/MEC: **Censo Escolar**, **IDEB** e **INSE** (ano de referência: 2023).

## 📦 Como baixar os dados

Os arquivos de dados brutos **não estão versionados neste repositório** (são grandes demais para o Git normal). Eles estão disponíveis na aba **Releases**, como anexos:

👉 **[Baixar os dados brutos (Release "dados-2023")](https://github.com/Bbenekko/ENG4402-Trabalho-Eng-de-dados/releases/tag/dados-2023)**

Na página da release, baixe os 5 arquivos:

| Arquivo | Tamanho | Origem |
|---|---|---|
| `microdados_ed_basica_2023.csv` | ~200 MB | Censo Escolar da Educação Básica 2023 (INEP) |
| `divulgacao_anos_iniciais_escolas_2025.xlsx` | ~53 MB | IDEB — Anos Iniciais do Ensino Fundamental (INEP) |
| `divulgacao_anos_finais_escolas_2025.xlsx` | ~37 MB | IDEB — Anos Finais do Ensino Fundamental (INEP) |
| `divulgacao_ensino_medio_escolas_2025.xlsx` | ~8,4 MB | IDEB — Ensino Médio (INEP) |
| `INSE_2023_escolas.xlsx` | ~8,4 MB | Indicador de Nível Socioeconômico das Escolas (INEP) |

## 📁 Onde colocar os arquivos baixados

Depois de baixar, coloque cada arquivo na pasta correspondente do repositório, seguindo exatamente esta estrutura (essas pastas já existem no repo, só estão vazias por causa do `.gitignore`):

```
Data/
├── Censo/
│   └── dados/
│       └── microdados_ed_basica_2023.csv          ← colocar aqui
├── INDEB/
│   ├── divulgacao_anos_iniciais_escolas_2025/
│   │   └── divulgacao_anos_iniciais_escolas_2025.xlsx   ← colocar aqui
│   ├── divulgacao_anos_finais_escolas_2025/
│   │   └── divulgacao_anos_finais_escolas_2025.xlsx     ← colocar aqui
│   └── divulgacao_ensino_medio_escolas_2025/
│       └── divulgacao_ensino_medio_escolas_2025.xlsx    ← colocar aqui
└── INSE/
    └── INSE_2023_escolas.xlsx                       ← colocar aqui
```

> ⚠️ Essas 5 localizações estão listadas no `.gitignore` do projeto — ou seja, mesmo depois de colocar os arquivos aí, o Git **não vai tentar versioná-los de novo**. Isso é proposital: os dados ficam disponíveis pra todo mundo via Release, sem pesar o histórico do repositório.

## 🗂 O que já vem no repositório (não precisa baixar)

Documentação de apoio dos datasets, que já está commitada:

- `Data/Censo/Anexos/ANEXO I - Dicionário de Dados/` — dicionário de colunas do Censo Escolar
- `Data/Censo/Anexos/ANEXO II - Questionários do Censo da Educação Básica/` — PDFs dos formulários (Aluno, Escola, Gestor Escolar, Profissional Escolar, Turma)
- `Data/Censo/leia-me/Leia-me.pdf` — notas de uso do Censo Escolar
- Aba **"Dicionário"** dentro do próprio `INSE_2023_escolas.xlsx` (depois de baixado) — explica as colunas do INSE

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
