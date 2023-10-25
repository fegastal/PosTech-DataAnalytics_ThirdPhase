# FASE 03 - AULA 12 - CLUSTERING COM BIGQUERY ML

Anotações sobre a décima segunda aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=338019&c=9543&sesskey=ihJRxGi0N1](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=338019&c=9543&sesskey=ihJRxGi0N1)

Temas abordados:

- Clustering de dados no ambiente Google BigQuery. Clustering é uma técnica de análise que *agrupa itens similares com base em suas características*, permitindo identificar padrões e tomar decisões estratégicas.
- Google BigQuery é um serviço eficiente e escalável de armazenamento e análise de dados, que oferece consultas rápidas e insights em tempo real.
- Exploramos alguns conceitos fundamentais do clustering, desde os algoritmos mais populares até as melhores práticas de pré-processamento de dados.
- Também conhecemos as funcionalidades do BigQuery, aplicando esses conceitos em projetos práticos.

---

## Introdução | O QUE É CLUSTERING DE DADOS?

Clustering, no contexto de ML, é uma técnica usada para agrupar objetos ou exemplos de dados *similares em grupos*, também conhecidos como clusters. O objetivo principal é **encontrar padrões intrínsecos nos dados, sem a necessidade de rótulos prévios ou supervisão**.

O processo de clustering envolve a atribuição de pontos de dados a grupos com base em sua similaridade. A similaridade é medida usando uma **função de distância ou similaridade**, que **quantifica quão próximos ou semelhantes dois pontos de dados estão entre si**. 

Os pontos de dados que são mais próximos uns dos outros têm uma maior similaridade e são agrupados juntos.

Existem vários algoritmos de clustering disponíveis, cada um com suas próprias abordagens e suposições sobre a estrutura dos dados. Alguns dos algoritmos de clustering mais comuns são o **K-means, o DBSCAN (Density-Based Spatial Clustering of Applications with Noise) e o Hierarchical Clustering**.

**K-means** → um dos mais amplamente utilizados. Atribui pontos de dados à clusters de forma interativa, minimizando a soma dos quadrados das distâncias entre os pontos e os centroides dos clusters. O número de clusters é especificado antecipadamente no K-means.

**DBSCAN** → baseado em densidade que agrupa pontos de dados em regiões densas do espaço. Ele não requer um número pré-definido de clusters e pode identificar automaticamente o número correto com base na densidade dos dados.

**Hierarchical Clustering** → cria uma hierarquia de clusters, formando uma árvore de clusters. Ele pode ser aglomerativo (começando com clusters individuais e mesclando-os) ou divisivo (começando com um cluster único e dividindo-o em subclusters).

O clustering tem várias aplicações em ML e análise de dados. Pode ser usado para segmentação de clientes, agrupamento de documentos, análise de redes sociais, detecção de anomalias entre outros.

Essa técnica ajuda a identificar grupos naturais dos dados, permitindo uma melhor compreensão e organização dos mesmos.

---

## Parte 1 | MÃO NA MASSA COM BIGQUERY ML

BigQuery tem vários conjuntos de dados de demonstração gratuitos. Nesse exemplo específico, usaremos o conjunto de dados “London Bicycle Hire” para construir o agrupamento K-means.

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled.png)

1 | Encontre “+ADD DATA” no painel esquerdo em “Explore public datasets”

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%201.png)

2 | Pesquise por “London Bicycle Hires” e clique em “View dataset”

A partir daí, você pode ver o banco de dados “bigquery-public-data”, adicionado no canto inferior esquerdo. Se você ver “london_bicycles” ao rolar para baixo, então estamos prontos(as).

3 | Para criar um modelo de agrupamento K-means no BigQuery, precisamos criar um “Dataset” que salve o modelo que iremos construir.

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%202.png)

Para fazer isso, clique no ID do projeto que você criou na etapa 1 e, em seguida, clique em “CREATE DATA-SET” no lado direito do monitor, conforme a imagem acima.

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%203.png)

4 | Coloque “k_means_tutorial” em DataSet ID e certifique-se de escolher ‘ EU ‘ em Data Location (os dados da bicicleta de Londres são armazenados na multirregião da EU (União Europeia). Portanto, esse conjunto de dados também deve estar localizado na mesma região).  Deixe as outras configs como estão e clique em “Criar conjunto de dados”.

Como mencionado anteriormente, o dataset que vamos usar é “**london_bicycledataset**” e vamos agrupar a estação de bicicletas por 3 das seguintes características:

1 → Duração do aluguel

2 → Número de aluguéis diários

3 → Distância da cidade

‘**london_bicyclesdataset**’ tem duas tabelas (**cycle_hire e cicly_stations**). Você pode clicar em cada conjunto de dados para ver as colunas de cada tabela.

**cycle_hire** → tabela de aluguel que tem rental_id e bike_id como sua chave e tem informações de duração e estação inicial / final para cada aluguel de bicicleta.

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%204.png)

**cycle_stations** → dados para a estação de aluguel de bicicletas (longitude / latitude e número de bicicletas para cada estação).

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%205.png)

As variáveis que usaremos para agrupas as estações são:

→ Duração do aluguel

→ Número de aluguéis diários

→ Distância da cidade

Passe o mouse sobre o projeto ‘k_means_tutorial’ que criamos e copie e cole a consulta SQL abaixo no editor de consultas e clique em ‘Executar’:

```sql
with hs as (
select
h.start_station_name as station_name
,if (extract(dayofweek from h.start_date) = 7 or
extract(dayofweek from h.start_date) = 1,
"weekend","weekday") as isweekday
,h.duration
,st_distance(st_geogpoint(s.longitude, s.latitude), st_geogpoint(-0.1, 51.5)) / 1000 as distance_from_city_center
from bigquery-public-data.london_bicycles.cycle_hireas h
join bigquery-public-data.london_bicycles.cycle_stationsas s
on h.start_station_id = [s.id](http://s.id/)
where h.start_date between cast('2015-01-01 00:00:00' as timestamp) and
cast('2016-01-01 00:00:00' as timestamp)
),
stationstats as (
select
station_name
,avg(duration) as duration
,count(duration) as num_trips
,max(distance_from_city_center) as distance_from_city_center
from hs
group by station_name
)
```

```sql
select *
from stationstats
order by distance_from_city_center
```

Depois disso, você deve ver algo como o que está na figura ‘Query results’, na seção ‘Resultados da consulta’

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%206.png)

O que está sendo realizado nesta consulta SQL:

→ Criamos duas tabelas temporárias ‘hs’ e ‘stationstats’ como subconsulta

→ ‘hs’ fornece as informações em cada linha para as estações em 2015 (nome, dia da semana, duração do aluguel, distância da cidade)

→ Em seguida, na tabela ‘stationstats’, usamos funções agregadas para calcular algumas estatísticas importantes armazenadas na tabela ‘hs’.

Agora que entendemos a logística básica do BigQuery, podemos criar um modelo de agrupamento K-means.

Podemos fazer um create model e com model_type = ‘kmeans’, treinaremos o modelo de agrupamento.

Copie e cole abaixo novamente e clique em ‘Executar’.

```sql
create or replace model
k_means_tutorial.london_station_clusters OPTIONS(model_type='kmeans',num_clusters=4) as
with hs as (
select
h.start_station_name as station_name
,if (extract(dayofweek from h.start_date) = 7 or
extract(dayofweek from h.start_date) = 1,
"weekend","weekday") as isweekday
,h.duration
,st_distance(st_geogpoint(s.longitude, s.latitude), st_geogpoint(-0.1, 51.5)) / 1000 as distance_from_city_center
from bigquery-public-data.london_bicycles.cycle_hireas h
join bigquery-public-data.london_bicycles.cycle_stationsas s
on h.start_station_id = [s.id](http://s.id/)
where h.start_date between cast('2015-01-01 00:00:00' as timestamp) and
cast('2016-01-01 00:00:00' as timestamp)
),
stationstats as (
select
station_name
, isweekday
,avg(duration) as duration
,count(duration) as num_trips
,max(distance_from_city_center) as distance_from_city_center
from hs
group by station_name, isweekday
)
select * except(station_name, isweekday)
from stationstats
order by distance_from_city_center
```

Esta consulta SQL difere da anterior em apenas duas partes:

→ Adicionamos uma linha para criar um modelo no conjunto de dados k_means_tutorial que criamos acima e o resultado é armazenado como ‘london_station_clusters’

```sql
create or replace model
bqml_tutorial.london_station_clusters options (model_type='kmeans',num_clusters=4) as
```

→ Adicionada uma nova coluna ‘isweekday’ na consulta ‘groupby’ na tabela stationstats e também adicionado except (station_name, isweekday). Para isso, queremos ver como o dia da semana / fim de semana afeta a taxa de aluguel. Além disso, a consulta Exceto (coluna) exclui os nomes das colunas dentro dos parênteses.

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%207.png)

Uma vez feito, você deve ver algo como a tela da figura “Go to model”. Clique em ‘Ir para o modelo’ (go to model) e verifique os detalhes.

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%208.png)

Se você clicar em “Esquema” (Schema), poderá ver que o modelo é treinado usando três colunas (duration, num_tips, distance_from_city_center).

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%209.png)

Se você clicar em “Avaliação” (Evaluation), poderá ver cada cluster. Temos 4 clusters desde que definimos num_clusters como 4 em create model, e vemos “valor do centroide”.

Vamos usar a função interna ‘ml.predict’ para encontrar o cluster ao qual uma determinada estação pertence.

```sql
with hs as (
select
h.start_station_name as station_name
,if (extract(dayofweek from h.start_date) = 7 or
extract(dayofweek from h.start_date) = 1,
"weekend","weekday") as isweekday
,h.duration
,st_distance(st_geogpoint(s.longitude, s.latitude), st_geogpoint(-0.1, 51.5)) / 1000 as distance_from_city_center
from bigquery-public-data.london_bicycles.cycle_hireas h
join bigquery-public-data.london_bicycles.cycle_stationsas s
on h.start_station_id = [s.id](http://s.id/)
where h.start_date between cast('2015-01-01 00:00:00' as timestamp) and
cast('2016-01-01 00:00:00' as timestamp)
),
stationstats as (
select
station_name
, isweekday
,avg(duration) as duration
,count(duration) as num_trips
,max(distance_from_city_center) as distance_from_city_center
from hs
group by station_name, isweekday
)
select * except(nearest_centroids_distance)
from ml.predict(
model k_means_tutorial.london_station_clusters,
(
select *
from stationstats
)
)
```

A consulta acima tem duas partes:

→ Modelo de agrupamento K-means que criamos.

→ Dados do conjunto de teste (para previsão).

Adicionamos **except (nearest_centroids_distance) para ver apenas os clusters previstos**.

![Untitled](FASE%2003%20-%20AULA%2012%20-%20CLUSTERING%20COM%20BIGQUERY%20ML%2064e15ea9677a414ea22a273e339a8be9/Untitled%2010.png)

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Qual é a linguagem de consulta utilizada em Graph Databases?

A) SQL

B) GraphQL

**C) Cypher**

D) Python

E) JSON

2 - O que é o GraphQL?

A) Uma linguagem de consulta para bancos de dados relacionais

B) Uma linguagem de consulta para bancos de dados gráficos

C) Uma linguagem de consulta para bancos de dados colunares

D) Uma linguagem de consulta para bancos de dados NoSQL

**E) Uma linguagem de consulta e manipulação de APIs**

3 - Qual dos seguintes bancos de dados é um exemplo de Graph Database?

A) MySQL

B) Cassandra

C) PostgreSQL

D) MongoDB

**E) Neo4j**

4 - Qual a principal vantagem de usar um Graph Database?

A) Armazenamento de grandes volumes de dados

B) Escalabilidade horizontal

C) Flexibilidade no esquema dos dados

D) Alta velocidade de leitura

**E) Representação e consulta eficiente de relacionamos complexos**

5 - O que é Graph Database?

A) Um banco de dados que utiliza o modelo de dados colunar para armazenamento

B) Um banco de dados que utiliza o modelo de documento para armazenamento

C) Um banco de dados relacional otimizado para consultas em grafo

D) Um banco de dados que utiliza o modelo de chave-valor para armazenamento

**E) Um banco de dados NoSQL que armazena dados em formato de gráfico**