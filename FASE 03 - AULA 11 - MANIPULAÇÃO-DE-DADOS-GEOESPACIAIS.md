# FASE 03 - AULA 11 - MANIPULAÇÃO DE DADOS GEOESPACIAIS

Anotações sobre a décima primeira aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337986&amp;sesskey=aUi3fmwArb](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=338018&c=9543&sesskey=ihJRxGi0N1)

Temas abordados:

- Aplicar de maneira prática os conceitos de dados geoespaciais dentro do Google BigQuery e entender como dados geográficos podem gerar valor através da manipulação com a linguagem SQL.

---

## Introdução | Entendendo sobre Dados Geoespaciais

Dados Geoespaciais são informações que possuem um componente geográfico ou de localização. São dados associados a coordenadas geográficas, como latitude e longitude, e representam características ou eventos que ocorrem em um determinado espaço geográfico.

Dados espaciais descrevem a localização, forma, tamanho e distribuição de objetos ou fenômenos na Terra ou em outros corpos celestes. Eles podem ser representados de várias formas, como pontos, linhas, polígonos ou superfícies.

Diferentes tipos de dados espaciais:

1 | Pontos → representam uma localização específica no espaço, como a posição de uma cidade, uma loja ou um sinal de GPS

2 | Linhas → sequência ordenada de pontos conectados, como estradas, rios ou rotas de voo

3 | Polígonos → representam uma área fechada definida por uma série de linhas, como fronteiras de países, estados ou regiões

4 | Superfícies → representam dados que cobrem uma área contínua, como modelos digitais de terreno, mapas de elevação ou imagens de satélite

Dados espaciais permitem visualizar, analisar e tomar decisões com base na dimensão geográfica, relacionando informações a locais específicos.

Ao trabalhar com dados espaciais, é possível realizar análises espaciais, como identificar padrões, calcular distâncias, realizar sobreposições de áreas, análise de proximidade, roteamento e muito mais.

Essas análises podem fornecer insights valiosos para entender a distribuição espacial de eventos, padrões geográficos e relações entre diferentes fenômenos.

Avanço da tecnologia → dados espaciais se tornam cada vez mais acessíveis e abundantes. Isso é impulsionado por fontes como sistemas de posicionamento global (GPS), imagens de satélite, sensores remotos, dispositivos móveis e redes de sensores. Esses avanços permitem uma melhor compreensão do mundo em que vivemos e o uso efetivo de dados geoespaciais para tomar decisões informadas em várias áreas de aplicação.

---

## Parte 1 | TRABALHANDO COM DADOS GEOESPACIAIS DENTRO DO GOOGLE BIGQUERY

→ Esse laboratório usa um conjunto de dados disponível por meio do Google Cloud Public Dataset Program. 

→ Um conjunto de dados público é qualquer conjunto de dados armazenado no BigQuery e disponibilizado ao público em geral.

→ Os conjuntos de dados públicos são conjuntos de dados que o BigQuery hospeda para você acessar e integrar em seus aplicativos.

→ O Google paga pelo armazenamento desses conjuntos de dados e fornece acesso público aos dados por meio de um projeto. Você paga apenas pelas consultas que realiza nos dados (o primeiro 1TB por mês é gratuito, sujeito aos detalhes de preço da consulta).

---

## Parte 2 | EXEMPLOS DE ALGUMAS LINHAS DE DADOS

Você pode começar a explorar dados no console do BigQuery visualizando os detalhes da *citibike_stationstabela:*

1 | Abra a IU da Web do BigQuery no Console do Google Cloud

2 | Selecione Menu de Navegação () > BigQuery

3 | A caixa de mensagem “Welcome to BigQuery” in the Cloud Console é aberta. Essa caixa de mensagem fornece um link para o guia de início rápido e lista as atualizações da interface do usuário.

4 | Clique em “Concluído”

5 | Consulte algumas linhas de bigquery-public-data.new_york_citibike_stations para entender os dados armazenados na tabela. Adicione a seguinte consulta à área de texto do editor de consultas:

```jsx
SELECT *
FROM bigquery-public-data.new_york_citibike.citibike_stations
LIMIT 10
```

![Untitled](FASE%2003%20-%20AULA%2011%20-%20MANIPULAC%CC%A7A%CC%83O%20DE%20DADOS%20GEOESPA%2064e15ea9677a414ea22a273e339a8be9/Untitled.png)

Três colunas são relevantes nessa tabela:

1 → Longitude → os valores são longitudes WGS 84 válidas no formato de graus decimais

2 → Latitude → os valores são latitudes WGS 84 válidas no formato de graus decimais

3 → num_bikes_available → número de bicicletas disponíveis para locação

Encontre as estações com mais de 30 bicicletas disponíveis e, em seguida, execute uma consulta SQL padrão que encontre todas as estações Citi Bike na cidade de Nova York com mais de 30 bicicletas disponíveis para aluguel.

1 → A consulta SQL padrão a seguir é usada para localizar as estações Citi Bike com mais de 30 bicicletas. Add esta consulta à área de texto do editor de consultas:

```jsx
SELECT
ST_GeogPoint(longitude, latitude)  AS WKT,
num_bikes_available
FROM bigquery-public-data.new_york.citibike_stations
WHERE num_bikes_available > 30
```

SELECT ST_GeogPoint(longitude, latitude) AS WKT, num_bikes_available A SELECT - cláusula seleciona a num_bikes_availablecoluna e usa a ST_GeogPoint - função para converter os valores nas colunas de latitude e longitude em GEOGRAPHYtipos (pontos).

FROM bigquery-public-data.new_york.citibike_stations A FROM - cláusula especifica a tabela que está sendo consultada: citibike_stations.

WHERE num_bikes_available > 30 A WHERE - cláusula filtra os valores na num_bikes_availablecoluna apenas para as estações com mais de 30 bicicletas.

1.	Clique no botão Executar para executar a consulta.

A consulta leva um momento para ser concluída. Após a execução da consulta, seus resultados aparecem no painel Resultados da consulta.

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Qual biblioteca Python é comumente usada para manipulação de dados geoespaciais?

A) GeoPy

B) Seaborn

**C) GeoPandas**
D) Pandas

E) NumPy

2 - Qual tipo de dado é usado para representar coordenadas geoespaciais no formato de latitude e longitude em Python?

**A) Tuple**
B) LineString
C) Polygon

D) Point
****E) String

3 - Qual método Python é usado para realizar uma consulta espacial em um banco de dados geoespacial?

A) execute_query()

B) fetchall()

C) geo_query()

D) spatial_query()
**E) ST_Intersects()**

4 -Qual dos seguintes bancos de dados é amplamente utilizado para armazenar e consultar dados geoespaciais?

A) MongoDB

B) MongoDB

C) MySQL

**D) PostgreSQL**

E) SQLite

5 - Qual das seguintes opções é uma estrutura de dados frequentemente usada para representar informações geoespaciais?

**A) Shapefile**

B) CSV
C) DataFrames

D) JSON
****E) XML

---