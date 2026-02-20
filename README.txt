# Segmentação de Clientes com Machine Learning (Python + Power BI)

## Descrição
Este projeto utiliza dados fictícios de clientes para realizar **segmentação de mercado** com base em idade, renda anual e pontuação de gastos.  
O objetivo é agrupar os clientes em **3 segmentos distintos** e gerar um relatório visual no **Power BI**, permitindo que a área de Marketing personalize campanhas e estratégias.

## Definição do Problema
A empresa deseja identificar grupos de clientes com características semelhantes para direcionar campanhas de Marketing.  
O desafio é aplicar **Machine Learning (K-Means)** para criar os clusters e disponibilizar um relatório com:
- Média de idade por segmento
- Média de renda anual por segmento
- Média de pontuação de gastos por segmento
- Total de clientes em cada segmento

## Dados
- **dados_clientes.csv**: dataset fictício com idade, renda anual e pontuação de gastos.  
- **segmentos.csv**: resultado da segmentação, incluindo o cluster atribuído a cada cliente.  

## Passo a Passo

### 1. Carregamento dos Dados

```python
# Verifica a versão da Linguagem Python

from platform import python_version
print('Versão da Linguagem Python Usada Neste Jupyter Notebook:', python_version())
```

# Importa os pacotes
import pandas as pd
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler
```

# Carrega os dados
df_dsa = pd.read_csv('dados/dados_clientes.csv')
```

# Verifica o tipo do objeto
type(df_dsa)
```

# Visualiza as 10 primeiras linhas
df_dsa.head(10)
```

### 2. Análise Exploratória

```python
# Resumo estatístico das variáveis para verificar consistência e distribuição dos dados
df_dsa[['idade', 'renda_anual', 'pontuacao_gastos']].describe()
```

### 3. Pré-Processamento

```python
# Cria o padronizador dos dados
padronizador = StandardScaler()

# Aplica o padronizador somente nas variáveis de interesse
dados_padronizados = padronizador.fit_transform(df_dsa[['idade', 'renda_anual', 'pontuacao_gastos']])


# Visualiza os dados
print(dados_padronizados)
```

### 4. Construção do Modelo

```python
# Definição do número de clusters (k).
k = 3

# Cria o modelo K-means
kmeans = KMeans(n_clusters = k)

# Treina o modelo com os dados padronizados
kmeans.fit(dados_padronizados)

# Atribuí os rótulos dos clusters aos clientes
df_dsa['cluster'] = kmeans.labels_

# Exibe o resultado (10 primeiras linhas)
df_dsa.head(10)

# Salva o resultado em disco
df_dsa.to_csv('dados/segmentos.csv', index = False)

```
### 5. Relatório no Power BI

O resultado da segmentação foi importado para o Power BI Desktop e visualizado em dashboards, incluindo:

- Média de idade por segmento
- Média de renda anual por segmento
- Média de pontuação de gastos por segmento
- Distribuição de clientes por cluster

![Dashboard Power BI](imagens/dashboard.png)

### Resultados
- Segmento 0: clientes com maior renda anual média.
- Segmento 1: clientes com maior pontuação de gastos.
- Segmento 2: clientes mais jovens, com renda e gastos intermediários.
Esses insights permitem que a área de Marketing direcione campanhas específicas para cada perfil de cliente

### Ferramentas Utilizadas
- Python (Pandas, Scikit-learn)
- Jupyter Notebook
- Power BI Desktop



