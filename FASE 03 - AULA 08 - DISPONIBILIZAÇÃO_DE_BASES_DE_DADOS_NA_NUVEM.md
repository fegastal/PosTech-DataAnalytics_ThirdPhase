# FASE 03 - AULA 08 - DISPONIBILIZAÇÃO DE BASES DE DADOS NA NUVEM

Anotações sobre a oitava aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337986&amp;sesskey=aUi3fmwArb](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=338015&c=9543&sesskey=s1k1poBKHM)

Temas abordados:

- Entender melhor o funcionamento do Google Cloud Platform e todos os seus principais componentes para construção de uma arquitetura de dados voltada para nuvem.
- Aprofundar ainda mais dentro dos conceitos e práticas de uso de SQL dentro do Google BigQuery.

---

## Introdução

Essa ferramenta (Google Cloud Platform) pode simplificar e aprimorar a gestão de dados em escala empresarial. A quantidade de dados gerados atualmente é em escala colossal, tornando-se um desafio **gerenciar e extrair insights valiosos** dessa imensa quantidade de informações.

É aí que a computação em nuvem e o Google BigQuery se tornou uma das soluções mais populares para a disponibilização de base de dados na nuvem.

Aprenderemos desde o básico, até as funcionalidades mais avançadas do Google BigQuery, permitindo explorar todo o potencial dessa plataforma. Abordaremos temas como criação de projetos e datasets, carregamento de dados, definição de esquemas e execução de consultas SQL poderosas.

Vamos também otimizar consultas, compartilhar dados com segurança, integrar o BigQuery a outras ferramentas do ecossistema do Google Cloud Platform e aproveitar recursos avançados, como **aprendizado de máquina e análise preditiva**. 

---

## Parte 1 | ENTENDENDO MELHOR O FUNCIONAMENTO DO GOOGLE CLOUD PLATFORM

![Untitled](FASE%2003%20-%20AULA%2008%20-%20DISPONIBILIZAC%CC%A7A%CC%83O%20DE%20BASES%20DE%2064e15ea9677a414ea22a273e339a8be9/Untitled.png)

Tem o conceito de Arquitetura de Dados Moderna focada principalmente na Google Cloud Platform. Podemos notar o papel que o BigQuery desempenha neste tipo de solução; o motor de consulta de dados massivamente com alto poder de processamento.

Funcionamento completo do BigQuery integrado com essas soluções nativas em nuvem:

**1 | GOOGLE CLOUD STORAGE (GCS)**

→ O GCS é um serviço de armazenamento de objetos altamente escalável no GCP.

→ Você pode carregar arquivos de dados diretamente no GCS, seja de fontes internas ou externas ao GCP.

→ O BigQuery pode ler dados armazenados no GCS como uma fonte de dados para processamento e análise.

**2 | CARREGAMENTO DE DADOS NO BIGQUERY**

→ Após armazenar seus arquivos de dados no GCS, você pode carregá-los no BigQuery.

→ O BigQuery oferece várias opções de carregamento, incluindo carregamento de arquivos .csv, .json, Avro, Parquet entre outros.

→ Você pode carregar dados diretamente do GCS para o BigQuery usando comandos SQL ou APIs do BigQuery.

**3 | PREPARAÇÃO DE DADOS NO BIGQUERY**

→ O BigQuery permite executar transformações nos dados carregados por meio de consultas SQL.

→ Você pode utilizar operações de filtragem, agregação, junção de tabelas, criação de novas colunas e outros tipos de manipulação de dados.

→ Essas transformações podem ser aplicadas aos dados carregados ou a tabelas já existentes no BigQuery.

**4 | GOOGLE DATAFLOW**

→ É um serviço de processamento de dados em lote e em streaming no GCP.

→ Você pode usar oi Dataflow para executar transformações avançadas nos dados antes de carregá-los no BigQuery.

→ O Dataflow é integrado ao BigQuery, permitindo que você processe dados em escala e, em seguida, carregue-os diretamente no BigQuery para análise.

**5 | ANÁLISE DE DADOS NO BIGQUERY**

→ Após o carregamento e a preparação dos dados, você pode executar consultas SQL avançadas no BigQuery para analisar os dados armazenados.

→ O BigQuery é projetado para oferecer consultas rápidas e escaláveis, permitindo analisar grandes conjuntos de dados em questão de segundos ou minutos.

→ Você pode usar recursos como janelas temporais, funções analíticas, agregações, entre outros recursos avançados do SQL, para extrair insights dos dados.

6 **| LOOKER**

→ É uma plataforma de Business Intelligence (BI) e visualização de dados.

→ Pode ser integrado ao BigQuery para criar painéis interativos, relatórios e visualizações dos dados armazenados no BigQuery.

→ O looker oferece recursos avançados de criação de dashboards, geração de relatórios e compartilhamento de insights com a equipe.

Essas integrações permitem que você carregue, prepare, analise e visualize dados de maneira eficiente e escalável na nuvem, facilitando a obtenção de insights valiosos a partir dos seus dados.

---

### Parte 2 - REALIZANDO EXPLORAÇÕES E ANÁLISE DE DADOS AVANÇADA COM SQL NO GOOGLE BIGQUERY

BigQuery é um serviço de armazenamento e análise de dados na nuvem que suporta consultas SQL avançadas. Ele permite executar consultas sofisticadas para extrair informações úteis dos dados armazenados no BigQuery. Exemplos:

**1 | CONSULTAS COM JOIN**

Usar junções para combinar dados de várias tabelas com base em colunas em comum. Exemplo: suponha que você tenha duas tabelas: “Orders” e “Customers” e queira obter detalhes de pedidos juntamente com as informações do cliente correspondente. Você pode:

```jsx
SELECT o.order_id, o.order_date, c.customer_name
FROM Orders o
JOIN Customers c ON o.customer_id = c.customer_id
```

2 **| SUB-QUERY**

Subconsultas são aninhadas dentro de uma consulta principal. Elas podem ser realizadas para cálculos intermediários ou filtrar resultados com base em condições específicas.

Exemplo: querer obter todos os clientes que fizeram mais de 10 pedidos. A consulta pode ser assim:

```jsx
SELECT customer_id, customer_name
	FROM Customers
	WHERE customer_id IN (
		SELECT customer_id
		FROM Orders
		GROUP BY customer_id
		HAVING COUNT(order_id) > 10)
```

**3 | CONSULTAS COM AGGREGATION**

BigQuery oferece várias funções de agregação que permitem calcular estatísticas ou resumos dos dados. Exemplo: você pode usar a função SUM para calcular a soma de valores em uma coluna ou COUNT para contar o número de registros que atendem a uma determinada condição.

Exemplo que calcula a receita total por categoria de produto:

```jsx
SELECT product_category, SUM(revenue) AS total_revenue
	FROM Sales
	GROUP BY product_category
```

4 **| CONSULTAS COM FUNÇÃO JANELA (WINDOW FUNCTIONS)**

Permitem realizar cálculos em um conjunto de linhas que estão relacionadas a uma linha específica. Exemplo: você pode querer calcular a média móvel de uma série temporal. Exemplo para calcular a média móvel de 7 dias para as vendas diárias:

```jsx
SELECT sale_date, sales_amount,
AVG(sales_amount) OVER (ORDER BY sale_date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS moving_average
FROM DailySales
```

Estes são apenas alguns exemplos de consultas SQL avançadas para executar no Google BigQuery. Há recursos adicionais, como partições de tabela, clustering e suporte para dados geoespaciais, que permitem otimizar ainda mais suas consultas e análises.

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Quais são os benefícios da disponibilização de uma base de dados em uma infraestrutura de nuvem?

**A) Todas as opções anteriores.**

B) Maior velocidade no processamento de grandes volumes.

C) Menor custo de infraestrutura.
D) Maior segurança dos dados.

E) Maior escalabilidade e flexibilidade.

2 - Qual é a principal vantagem de utilizar uma infraestrutura de nuvem para a disponibilização de base de dados?

A) Maior controle sobre o hardware utilizado.
**B) Redução da carga operacional e manutenção da infraestrutura.**
C) Melhor desempenho devido à proximidade física com os usuários.
D) Menor tempo de processamento de consultas.
E) Menor risco de perda de dados.

3 - Qual das seguintes opções descreve corretamente a disponibilização de uma base de dados em uma infraestrutura de nuvem?

**A) Utilizar um serviço de base de dados em nuvem, como o Amazon RDS.**
B) Hospedar a base de dados em servidores físicos no local.
C) Utilizar uma plataforma de Big Data como o Apache Hadoop.
~~D) Utilizar um serviço de armazenamento em nuvem, como o Google Cloud Storage.~~
****E) Utilizar uma biblioteca de processamento de dados como o Apache Spark.

“*O Amazon Relational Database Service, ou Amazon RDS é um serviço de banco de dados relacional distribuído da Amazon Web Services. É um serviço da web executado "na nuvem" projetado para simplificar a configuração, operação e escalonamento de um banco de dados relacional para uso em aplicativos.”*

4 - Qual das seguintes opções é uma plataforma de infraestrutura de nuvem popular para disponibilização de base de dados?

A) Amazon Web Services (AWS).

**B) Todas as opções anteriores.**
C) Alibaba Cloud.
D) Google Cloud Platform (GCP).
E) Microsoft Azure.

5 - Qual é o principal desafio ao disponibilizar uma base de dados em uma infraestrutura de nuvem?

A) Dificuldade em escalar horizontalmente.

B) Falta de segurança dos dados.
C) Custos com migração de infraestrutura.

**D) Dependência de fornecedores de nuvem.**
E) Restrições de largura de banda.

---