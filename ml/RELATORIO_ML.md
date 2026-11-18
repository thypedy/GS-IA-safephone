# SafePhone — Relatório de Inteligência Artificial e Machine Learning

## 1. Problema e objetivo

O SafePhone é uma proposta CitizenTech voltada à prevenção de furtos e roubos de celulares na cidade de São Paulo. O projeto utiliza dados históricos para identificar padrões de ocorrências por bairro e período, contribuindo para a conscientização e prevenção dos cidadãos.

A pergunta de Machine Learning definida foi: **é possível estimar a quantidade de registros de furtos e roubos de celulares em determinado bairro e mês, utilizando informações históricas?**

O objetivo é desenvolver um modelo capaz de identificar padrões temporais e geográficos, oferecendo informações que possam apoiar a conscientização da população.

## 2. Fonte e preparação dos dados

Foram utilizados arquivos públicos de registros de celulares subtraídos, disponibilizados pela Secretaria da Segurança Pública do Estado de São Paulo (SSP-SP).

**Fonte:** https://www.portal.ssp.sp.gov.br/estatistica/consultas

**Período dos arquivos consultados:** 2022 a 2025.

Foram selecionadas aleatoriamente até 3.000 linhas de cada arquivo original, totalizando uma amostra inicial de até 12.000 registros. Em seguida, foram aplicados filtros para selecionar:

- Município de São Paulo;
- Objetos classificados como telefone celular;
- Ocorrências classificadas como furto ou roubo.

Os dados foram normalizados, as datas inválidas foram removidas e os boletins duplicados foram tratados. Posteriormente, os registros foram agrupados por bairro, ano e mês.

A base final possui 6.220 registros únicos e 933 bairros representados. Alguns registros possuem datas de ocorrência anteriores ao ano do arquivo consultado, incluindo 2020 e 2021.

Foram selecionados os 20 bairros com maior quantidade de registros no conjunto de treinamento, evitando utilizar informações de 2025 nessa seleção.

**Observação:** os resultados representam a amostra selecionada, não o total oficial de ocorrências da cidade. A amostragem limita a capacidade de generalizar as contagens para toda a população de registros.

## 3. Modelo e metodologia

Foi escolhido o algoritmo **Random Forest Regressor**, por sua capacidade de aprender relações não lineares, combinar variáveis numéricas e categóricas e reduzir a dependência de uma única árvore de decisão.

As variáveis utilizadas foram:

- **BAIRRO:** localização da ocorrência;
- **ANO:** ano da ocorrência;
- **MES:** mês da ocorrência.

A variável-alvo foi **TOTAL_OCORRENCIAS**, correspondente à quantidade de boletins únicos na combinação de bairro, ano e mês.

A divisão dos dados foi realizada temporalmente:

- **Treinamento:** 2022, 2023 e 2024;
- **Teste:** 2025.

Foi utilizado OneHotEncoder para transformar os bairros em variáveis numéricas, mantendo o pré-processamento dentro de um Pipeline.

## 4. Experimentos e avaliação

Foram testadas 12 combinações de três hiperparâmetros, utilizando validação cruzada com três divisões exclusivamente no conjunto de treinamento.

| Hiperparâmetro | Valores testados |
|---|---|
| n_estimators | 100 e 200 |
| max_depth | None e 10 |
| min_samples_split | 2, 5 e 10 |

A melhor configuração encontrada foi:

- **n_estimators:** 200;
- **max_depth:** 10;
- **min_samples_split:** 10.

O MAE médio da validação cruzada foi de aproximadamente **1,2315**.

### Comparação dos modelos no teste de 2025

| Modelo | MAE | RMSE | R² |
|---|---:|---:|---:|
| Modelo básico | 1,2326 | 1,5047 | -0,0235 |
| Random Forest com ANO | **1,0746** | **1,4047** | **0,1080** |
| Random Forest sem ANO | 1,1930 | 1,5302 | -0,0584 |

O Random Forest com a variável ANO apresentou o melhor resultado nas três métricas. Na análise de importância das variáveis, o mês apresentou a maior importância individual, seguido pelo ano.

O gráfico de valores reais versus previstos demonstrou que o modelo tende a aproximar suas previsões da média, apresentando dificuldades para identificar valores extremos.

### Comparação entre treinamento e teste

| Conjunto | MAE | RMSE | R² |
|---|---:|---:|---:|
| Treinamento | 1,0555 | 1,3428 | 0,4207 |
| Teste (2025) | 1,0746 | 1,4047 | 0,1080 |

### Análise de overfitting

O desempenho deve ser analisado considerando a diferença entre os resultados de treinamento e teste. O R² caiu de 0,4207 no treinamento para 0,1080 no teste, indicando perda de capacidade explicativa em dados não vistos.

Embora a diferença entre os erros absolutos seja pequena, a redução do R² indica que o modelo apresenta dificuldades de generalização. Portanto, há sinais de possível overfitting, mas sua capacidade preditiva ainda é limitada.

## 5. Conclusão e impacto para o cidadão

O projeto demonstrou a aplicação do ciclo de Machine Learning em dados públicos relacionados a furtos e roubos de celulares em São Paulo.

O Random Forest com as variáveis bairro, ano e mês apresentou desempenho superior ao modelo básico e à versão sem a variável ano. Entretanto, o R² de 0,1080 demonstra que ainda existem limitações importantes na capacidade preditiva.

Para o cidadão, a proposta do SafePhone é transformar informações históricas em indicadores que ajudem a compreender padrões de ocorrências e reforçar ações preventivas.

O modelo desenvolvido deve ser considerado experimental e não deve ser utilizado para afirmar o risco real de um bairro ou prever crimes individuais. Trabalhos futuros podem ampliar a quantidade de dados, incorporar variáveis temporais e geográficas adicionais e avaliar outros algoritmos.

**O SafePhone demonstra como dados públicos e Machine Learning podem contribuir para iniciativas de conscientização e prevenção, desde que suas limitações sejam consideradas.**