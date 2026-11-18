# Dados do projeto SafePhone

## 1. Fonte dos dados

Os dados utilizados neste projeto são provenientes de registros públicos de celulares subtraídos, disponibilizados pela Secretaria da Segurança Pública do Estado de São Paulo (SSP-SP).

**Fonte:** https://www.portal.ssp.sp.gov.br/estatistica/consultas

**Arquivos consultados:** 2022 a 2025.

**Observação:** alguns registros possuem datas de ocorrência anteriores ao ano do arquivo, incluindo registros de 2020 e 2021.

## 2. Arquivos originais

Os arquivos Excel utilizados foram:

- `CelularesSubtraidos_2022.xlsx`
- `CelularesSubtraidos_2023.xlsx`
- `CelularesSubtraidos_2024.xlsx`
- `CelularesSubtraidos_2025.xlsx`

## 3. Processamento dos dados

Para reduzir o tempo de processamento, foi utilizada uma amostragem aleatória de até 3.000 registros por arquivo, com sementes definidas para permitir a reprodução do procedimento.

Foram aplicados os seguintes filtros:

1. Município: São Paulo.
2. Tipo de objeto: telefone celular.
3. Classificação: furto, furto qualificado ou roubo.

Em seguida, foram realizadas as seguintes etapas:

- Normalização dos nomes dos bairros.
- Conversão e validação das datas.
- Remoção de registros com datas inválidas.
- Identificação e tratamento de boletins duplicados.
- Agrupamento por bairro, ano e mês.
- Seleção dos 20 bairros com maior quantidade de ocorrências no conjunto de treinamento.

## 4. Arquivos processados

Os arquivos Parquet armazenam os dados após a aplicação dos filtros:

- `safephone_2022.parquet`
- `safephone_2023.parquet`
- `safephone_2024.parquet`
- `safephone_2025.parquet`
- `safephone_base_limpa.parquet`

## 5. Contagem final

Após a limpeza e o tratamento de duplicidades, a base apresentou:

- Registros após limpeza: **6.220**
- Boletins únicos: **6.220**
- Bairros representados: **933**

Distribuição por ano de ocorrência:

| Ano | Ocorrências |
|---|---:|
| 2020 | 4 |
| 2021 | 29 |
| 2022 | 2.033 |
| 2023 | 1.396 |
| 2024 | 1.359 |
| 2025 | 1.399 |

## 6. Limitações

Os dados utilizados representam uma amostra dos arquivos originais, e não a totalidade dos registros oficiais.

Portanto, os resultados do modelo não devem ser interpretados como estimativas oficiais do número total de furtos e roubos de celulares em São Paulo.

A amostragem, os filtros aplicados e a disponibilidade dos registros podem influenciar os resultados e limitar sua generalização.