# SafePhone — Machine Learning

## 1. Sobre o projeto

O SafePhone é um projeto CitizenTech que utiliza Inteligência Artificial e Machine Learning para analisar padrões de furtos e roubos de celulares na cidade de São Paulo.

O objetivo é identificar padrões por bairro e período, contribuindo para a conscientização e prevenção de ocorrências.

## 2. Objetivo do modelo

O problema foi definido como uma tarefa de regressão:

**Estimar a quantidade de ocorrências de furto e roubo de celulares por bairro, ano e mês.**

O modelo utiliza informações históricas para identificar padrões temporais e geográficos.

## 3. Tecnologias utilizadas

- Python 3.12
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook
- Random Forest Regressor

## 4. Modelo de Machine Learning

Foi utilizado o algoritmo Random Forest Regressor.

As variáveis de entrada são:

- BAIRRO
- ANO
- MES

A variável de saída é TOTAL_OCORRENCIAS.

A base foi dividida temporalmente:

- Treinamento: 2022, 2023 e 2024.
- Teste: 2025.

Foram testadas 12 combinações de hiperparâmetros, utilizando validação cruzada com três divisões no conjunto de treinamento.

## 5. Resultados

O modelo Random Forest com a variável ANO apresentou os melhores resultados:

| Métrica | Resultado |
|---|---:|
| MAE | 1,0746 |
| RMSE | 1,4047 |
| R² | 0,1080 |

Os resultados indicam desempenho superior ao modelo básico, embora a capacidade de previsão ainda seja limitada.

## 6. Estrutura do projeto

```text
ML-GS2/
├── dados/
│   ├── arquivos Excel originais
│   ├── arquivos Parquet processados
│   └── README.md
│
└── ml/
    ├── safephone.ipynb
    ├── requirements.txt
    ├── prompts.md
    ├── README.md
    └── RELATORIO_ML.md
```

## 7. Como executar

### Instalar as dependências

```bash
pip install -r requirements.txt
```

### Executar o projeto

1. Abra a pasta do projeto no Visual Studio Code.
2. Selecione o interpretador Python.
3. Abra `safephone.ipynb`.
4. Execute as células na ordem apresentada.

Os arquivos originais devem estar disponíveis na pasta `dados/`.

## 8. Limitações

O modelo foi desenvolvido utilizando uma amostra aleatória dos registros públicos, e não a totalidade dos dados oficiais.

O R² de 0,1080 demonstra que o modelo ainda possui capacidade limitada para explicar a variação das ocorrências.

As previsões não representam riscos reais de criminalidade e não devem ser utilizadas para prever crimes individuais.

## 9. Possíveis melhorias futuras

- Ampliar a quantidade de dados utilizados.
- Incorporar novas variáveis temporais e geográficas.
- Testar outros algoritmos de Machine Learning.
- Melhorar a capacidade de generalização do modelo.
- Desenvolver recursos de conscientização para os cidadãos.