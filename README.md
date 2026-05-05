# Tech Challenge - Analise Brazilian E-Commerce

## Sobre o Projeto

Relatorio executivo voltado a investidores e acionistas do setor de e-commerce, baseado no **Brazilian E-Commerce Public Dataset by Olist**. Transformamos dados transacionais de ~100 mil pedidos (2016-2018) em uma narrativa clara sobre desempenho comercial, eficiencia logistica e satisfacao do cliente, com recomendacoes acionaveis e previsoes fundamentadas.

## KPIs Principais

| Indicador | Valor |
|---|---|
| Receita Total | R$ 15,7 milhoes |
| Total de Pedidos | 98.200 |
| Ticket Medio | R$ 160,24 |
| Clientes Unicos | 93.358 |
| Mediana Lead Time | 10,2 dias |
| Taxa de Atraso | 8,1% |
| Score Medio | 4,16 / 5,0 |
| NPS | 66,1 |
| Taxa de Recompra | 3,0% |

## Estrutura do Repositorio

```
olist_project/
├── README.md                  # Este arquivo
├── requirements.txt           # Dependencias Python
├── data/                      # Dataset Olist (CSVs)
│   ├── olist_customers_dataset.csv
│   ├── olist_orders_dataset.csv
│   ├── olist_order_items_dataset.csv
│   ├── olist_order_payments_dataset.csv
│   ├── olist_order_reviews_dataset.csv
│   ├── olist_products_dataset.csv
│   ├── olist_sellers_dataset.csv
│   ├── olist_geolocation_dataset.csv
│   └── product_category_name_translation.csv
├── src/                       # Codigo-fonte
│   ├── data_loader.py         # Modulo de carga e limpeza dos dados
│   ├── analise_completa.py    # Analise completa com geracao de 20 graficos
│   └── expansoes.py           # Expansoes: text mining, coorte, previsao, financeiro (7 graficos)
├── output/
│   ├── charts/                # 27 graficos gerados pela analise
│   └── reports/
│       └── RELATORIO_EXECUTIVO.md  # Relatorio executivo completo
└── docs/
    └── DICIONARIO_DADOS.md    # Dicionario de dados
```

## Trilhas Analiticas

### 1. Crescimento e Receita
- Evolucao mensal de pedidos, receita e ticket medio
- Top 10 categorias por receita
- Participacao por estado (UF)
- Top 10 sellers por receita

### 2. Logistica e SLA
- Distribuicao do tempo total de entrega
- Lead time por etapa (aprovacao, postagem, transporte)
- Correlacao entre atrasos e review score
- Taxa de atraso por estado
- Evolucao mensal do lead time

### 3. Comportamento e Pagamentos
- Meios de pagamento (transacoes e volume financeiro)
- Distribuicao de parcelas no cartao de credito
- Segmentacao RFM (Recencia, Frequencia, Monetizacao)
- Taxa de recompra

### 4. Satisfacao do Cliente
- Distribuicao de review scores
- Score medio por categoria
- Drivers de satisfacao (lead time e preco)
- Evolucao mensal do NPS

### 5. Oportunidades e Recomendacoes
- Frete como % do preco por categoria
- Matriz de performance dos sellers (Score vs Lead Time)
- Oportunidades de cross-sell
- Heatmap de receita Estado x Categoria
- Projecao de receita (tendencia linear)

## Como Executar

### Pre-requisitos

```bash
pip install -r requirements.txt
```

### Rodar a Analise

```bash
python src/analise_completa.py
```

Os graficos serao salvos em `output/charts/` e o relatorio esta em `output/reports/`.

## Tecnologias Utilizadas

- **Python 3.12**
- **pandas** - Manipulacao e analise de dados
- **matplotlib** - Visualizacoes estaticas
- **seaborn** - Visualizacoes estatisticas
- **numpy** - Computacao numerica
- **scipy** - Computacao cientifica

## Dataset

- **Fonte:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- **Periodo:** Setembro/2016 a Outubro/2018
- **Volume:** ~100.000 pedidos, 9 tabelas interconectadas
- **Dados:** Reais e anonimizados

## Autores

Tech Challenge - Pos-graduacao
