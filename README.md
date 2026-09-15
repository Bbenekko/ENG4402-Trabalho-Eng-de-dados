# ENG4402-Trabalho-Eng-de-dados

Projeto de modelagem relacional e ETL sobre educação básica brasileira, cruzando três fontes do INEP/MEC: **Censo Escolar**, **IDEB** e **INSE** (ano de referência: 2023).

## 📁 Estrutura do repositório

```
Data/
├── Censo/
│   ├── dados/                         ← CSV bruto 
│   ├── Anexos/                        ← dicionário de dados e questionários 
│   └── leia-me/                       ← notas de uso do INEP 
├── INDEB/
│   └── ideb_ensino_medio_2023.csv     ← CSV bruto 
└── INSE/
    └── INSE_2023_escolas.csv          ← CSV bruto 

## 🗂 Documentação de apoio (já vem no repositório)

- `Data/Censo/Anexos/ANEXO I - Dicionário de Dados/` — dicionário de colunas do Censo Escolar
- `Data/Censo/Anexos/ANEXO II - Questionários do Censo da Educação Básica/` — PDFs dos formulários (Aluno, Escola, Gestor Escolar, Profissional Escolar, Turma)
- `Data/Censo/leia-me/Leia-me.pdf` — notas de uso do Censo Escolar

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
