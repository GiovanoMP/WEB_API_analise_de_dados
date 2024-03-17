# Análise de Dados de Cervejarias com a API Open Brewery DB

Este projeto tem como objetivo demonstrar como obter e analisar dados de cervejarias utilizando a API Open Brewery DB. Realizamos uma consulta específica para cervejarias na cidade de Nova York e limitamos os resultados a 10 registros. Em seguida, salvamos esses dados em um arquivo JSON e realizamos uma análise inicial sobre os países representados nas cervejarias retornadas.

## Bibliotecas Utilizadas

- `requests`: Para fazer solicitações HTTP à API.
- `json`: Para manipular dados em formato JSON.
- `pandas`: Para análise e manipulação de dados.

## Metodologia

1. **Consulta à API Open Brewery DB**: Utilizamos a biblioteca `requests` para realizar uma solicitação HTTP GET à API, buscando por cervejarias na cidade de Nova York e limitando o resultado a 10 cervejarias.

2. **Salvamento dos Dados**: Os dados recebidos da API são salvos em um arquivo JSON, `brewery_data.json`, permitindo uma análise posterior e persistência dos dados.

3. **Análise de Dados**: Abriu-se o arquivo JSON para análise, utilizando o Python e a biblioteca `pandas` para converter os dados em um DataFrame. Isso facilitou a análise estatística inicial, como contar a ocorrência de países nas cervejarias listadas.

## Resultados

- Todos os registros obtidos eram de cervejarias localizadas nos Estados Unidos, como esperado devido ao parâmetro de busca por cervejarias em Nova York.

- O DataFrame criado permitiu uma visão clara da estrutura dos dados, facilitando análises futuras mais detalhadas.

## Código de Exemplo

Aqui está um exemplo básico do código utilizado para consultar a API, salvar os dados e realizar uma análise inicial:

```python
import requests
import json
import pandas as pd

# Consulta à API
api_url = "https://api.openbrewerydb.org/breweries"
params = {'by_city': 'new_york', 'per_page': 10}
req = requests.get(api_url, params=params)
data = req.json()

# Salvando os dados em um arquivo JSON
with open('brewery_data.json', 'w') as datafile:
    json.dump(data, datafile)

# Carregando e analisando os dados
with open('brewery_data.json', 'r') as datafile:
    data = json.load(datafile)

df = pd.DataFrame(data)
print(df.country.value_counts())
