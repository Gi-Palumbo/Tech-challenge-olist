# Dicionario de Dados - Brazilian E-Commerce Dataset

## Visao Geral

O dataset contem informacoes de ~100.000 pedidos realizados no e-commerce brasileiro entre setembro de 2016 e outubro de 2018. Os dados sao reais e foram anonimizados.

---

## Tabelas

### customers (olist_customers_dataset.csv)
Informacoes dos clientes.

| Coluna | Tipo | Descricao |
|---|---|---|
| customer_id | string | Chave do cliente no dataset de pedidos |
| customer_unique_id | string | Identificador unico do cliente (pode ter multiplos customer_id) |
| customer_zip_code_prefix | int | Primeiros 5 digitos do CEP |
| customer_city | string | Cidade do cliente |
| customer_state | string | Estado do cliente (UF) |

### orders (olist_orders_dataset.csv)
Tabela central de pedidos.

| Coluna | Tipo | Descricao |
|---|---|---|
| order_id | string | Identificador unico do pedido |
| customer_id | string | Chave para tabela customers |
| order_status | string | Status: delivered, shipped, canceled, etc. |
| order_purchase_timestamp | datetime | Momento da compra |
| order_approved_at | datetime | Momento da aprovacao do pagamento |
| order_delivered_carrier_date | datetime | Momento da postagem na transportadora |
| order_delivered_customer_date | datetime | Momento da entrega ao cliente |
| order_estimated_delivery_date | datetime | Data estimada de entrega |

### order_items (olist_order_items_dataset.csv)
Itens de cada pedido.

| Coluna | Tipo | Descricao |
|---|---|---|
| order_id | string | Identificador do pedido |
| order_item_id | int | Numero sequencial do item no pedido |
| product_id | string | Identificador do produto |
| seller_id | string | Identificador do vendedor |
| shipping_limit_date | datetime | Data limite para postagem |
| price | float | Preco do item (R$) |
| freight_value | float | Valor do frete do item (R$) |

### payments (olist_order_payments_dataset.csv)
Informacoes de pagamento.

| Coluna | Tipo | Descricao |
|---|---|---|
| order_id | string | Identificador do pedido |
| payment_sequential | int | Sequencia de pagamentos para o pedido |
| payment_type | string | Tipo: credit_card, boleto, voucher, debit_card |
| payment_installments | int | Numero de parcelas |
| payment_value | float | Valor do pagamento (R$) |

### order_reviews (olist_order_reviews_dataset.csv)
Avaliacoes dos clientes.

| Coluna | Tipo | Descricao |
|---|---|---|
| review_id | string | Identificador unico da avaliacao |
| order_id | string | Identificador do pedido |
| review_score | int | Score de 1 a 5 |
| review_comment_title | string | Titulo do comentario |
| review_comment_message | string | Texto do comentario |
| review_creation_date | datetime | Data de criacao |
| review_answer_timestamp | datetime | Data de resposta |

### products (olist_products_dataset.csv)
Catalogo de produtos.

| Coluna | Tipo | Descricao |
|---|---|---|
| product_id | string | Identificador unico do produto |
| product_category_name | string | Categoria (em portugues) |
| product_name_lenght | int | Comprimento do nome |
| product_description_lenght | int | Comprimento da descricao |
| product_photos_qty | int | Quantidade de fotos |
| product_weight_g | float | Peso em gramas |
| product_length_cm | float | Comprimento em cm |
| product_height_cm | float | Altura em cm |
| product_width_cm | float | Largura em cm |

### sellers (olist_sellers_dataset.csv)
Informacoes dos vendedores.

| Coluna | Tipo | Descricao |
|---|---|---|
| seller_id | string | Identificador unico do vendedor |
| seller_zip_code_prefix | int | CEP do vendedor |
| seller_city | string | Cidade do vendedor |
| seller_state | string | Estado do vendedor (UF) |

### geolocation (olist_geolocation_dataset.csv)
Geolocalizacao por CEP.

| Coluna | Tipo | Descricao |
|---|---|---|
| geolocation_zip_code_prefix | int | Primeiros 5 digitos do CEP |
| geolocation_lat | float | Latitude |
| geolocation_lng | float | Longitude |
| geolocation_city | string | Cidade |
| geolocation_state | string | Estado (UF) |

### category_translation (product_category_name_translation.csv)
Traducao de nomes de categorias.

| Coluna | Tipo | Descricao |
|---|---|---|
| product_category_name | string | Nome em portugues |
| product_category_name_english | string | Nome em ingles |

---

## Relacionamentos

```
customers ---< orders ---< order_items >--- products
                  |              |
                  |              >--- sellers
                  |
                  ---< payments
                  |
                  ---< order_reviews

geolocation (referencia por zip_code_prefix)
category_translation (referencia por product_category_name)
```

## Metricas Derivadas

| Metrica | Calculo |
|---|---|
| Lead Time Total | order_delivered_customer_date - order_purchase_timestamp |
| Lead Time Aprovacao | order_approved_at - order_purchase_timestamp |
| Lead Time Postagem | order_delivered_carrier_date - order_approved_at |
| Lead Time Transporte | order_delivered_customer_date - order_delivered_carrier_date |
| Atraso | order_delivered_customer_date - order_estimated_delivery_date |
| Ticket Medio | Soma(price + freight) / Count(orders) |
| NPS | (% scores 4-5) - (% scores 1-2) |
| Taxa de Recompra | Clientes com >1 pedido / Total clientes unicos |
| RFM Score | Combinacao de Recencia + Frequencia + Monetizacao |
