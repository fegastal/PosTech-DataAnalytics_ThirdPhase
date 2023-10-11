# FASE 03 - AULA 03 - CONSULTAS E SELEÇÕES

Anotações sobre a terceira aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=307799&c=8729&sesskey=mp0PcE8JII](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337983&amp;sesskey=7rr89OBC9S)

Temas abordados:

- Criação de tabelas temporárias e visualizações, até a aplicação de cláusulas de filtragem, ordenação e agregação.
- Praticar consultas e seleções utilizando a linguagem de programação SQL ou DSL (Domain-Specific Language) do Spark.
- Escrever consultas eficientes e utilizar poderosas funções do Apache para processar e manipular dados em escala.

---

## Parte 1 | SPARK SQL

Spark SQL é um módulo do Apache Spark (poderoso framework de processamento distribuído e análise de dados em larga escala).

→ Permite que as pessoas desenvolvedoras trabalhem com dados estruturados usando SQL (Structured Query Language) e com datasets distribuídos, combinando os benefícios do **processamento em lote e em tempo real**.

→ **Fornece uma API unificada** para trabalhar com dados estruturados, permitindo que os devs usem consultas SQL tradicionais, juntamente com recursos avançados de análise de dados.

→ Suporta ampla variedade de fontes de dados, incluindo arquivos .csv, .json, Parquet, bancos de dados relacionais e muito mais.

→ O SparkSQL pode ser integrado a outros componentes do ecossistema Spark, como o Spark Streaming, MLlib e GraphX.

![Untitled](FASE%2003%20-%20AULA%2003%20-%20CONSULTAS%20E%20SELEC%CC%A7O%CC%83ES%206444fa2be0574c76abadaa0d27805196/Untitled.png)

Fig. 1 - SparkSQL

- Principais vantagens:

→ Capacidade de realizar otimizações de consulta para melhorar o desempenho com um otimizador de consultas que pode analisar consultas SQL, otimizá-las e gerar um plano de execução eficiente.

→ Também pode aproveitar a execução distribuída para processar consultas em paralelo em um cluster de computadores, o que permite lidar com grandes volumes de dados de maneira escalável e eficiente.

→ Capacidade de executar operações de processamento de dados complexas, como agregações, junções, filtros e transformações, tanto em dados estruturados quanto em dados semiestruturados. 

→ Também suporta funções de agregação personalizadas, permitindo que os desenvolvedores definam suas próprias operações de resumo de dados.

→ Oferece suporte a DataFrames e Datasets, que são abstrações de alto nível para manipulação de dados, de acordo com a linguagem de programação escolhida.

→ DataFrames são estruturas de dados imutáveis semelhantes a tabelas em um banco de dados relacional.

→ Datasets são uma extensão dos DataFrames, que fornecem uma interface tipada para manipulação de dados usando a linguagem Scala, Java ou Python.

→ O Spark SQL é amplamente utilizado em vários cenários, como análise de dados, processamento de logs, business intelligence e data warehousing. 

→ Sua combinação de recursos SQL, processamento distribuído e otimizações de consultas torna-o uma escolha popular para lidar com grandes volumes de dados em ambientes distribuídos.

→ Spark SQL é um componente essencial do ecossistema Spark, fornecendo recursos avançados para consulta, análise e processamento distribuído de dados estruturados.

→ Sua API unificada e capacidades de otimização de consultas o tornam uma ferramenta poderosa para lidar com análises de dados em grande escala.

---

**COMPONENTES DO SPARK SQL**

Dois principais componentes são o DataFrame e o SQLContext contidos.

![Untitled](FASE%2003%20-%20AULA%2003%20-%20CONSULTAS%20E%20SELEC%CC%A7O%CC%83ES%206444fa2be0574c76abadaa0d27805196/Untitled%201.png)

O foco será no principal componente de SparkSQL, que é o DataFrame.

É uma coleção de dados distribuídos e organizados em forma de COLUNAS NOMEADAS. É baseado no conceito de estrutura de dados da linguagem R, similar a uma tabela de um banco de dados relacional. 

Antes da versão 1.3, o componente DataFrame era chamado de **SchemaRDD**. DataFrames podem ser transformados em RDDs por meio de uma chamada de método RDD, que retorna o conteúdo de um DataFrame como um conjunto de linhas RDD.

DataFrames podem ser criados a partir de diferentes fontes de informações, como:

1 *RDDs já existentes;*

2 *Arquivos de dados estruturados;*

3 *Conjuntos de dados JSON;*

4 *Tabelas Hive;*

5 *Banco de dados externos;*

Linguagens de programação disponíveis: Scala, Java e Python.

---

### **SQLContext**

É uma interface que permite executar **consultas e seleções de dados** usando a linguagem SQL em conjuntos de dados distribuídos, como RDDs (Resilient Distributed Datasets) ou DataFrames.

O SQLContext fornece uma maneira convincente de trabalhar com **dados estruturados** usando a **sintaxe familiar do SQL**. 

→ Importando as bibliotecas necessárias

```jsx
from pyspark.sql import SparkSession
```

→ Criando uma SparkSession e um SQLContext → Criamos uma instância de “SparkSession” usando “SparkSession.builder” e obtendo ou criando uma sessão existente. A partir da sessão Spark, obtemos o “sqlContext” para acessar as funcionalidades do SQL.

```jsx
spark = SparkSession.builder.getOrCreate()
sqlContext = spark.sqlContext
```

→ Carregando um arquivo CSV como DataFrame → especificar o caminho do arquivo, indicando que a primeira linha é o cabeçalho e permitindo que o Spark inferisse o esquema dos dados.

```jsx
df = spark.read.csv(”caminho/do/arquivo.csv”, header=True, inferSchema=True)
```

→ Registrando o DataFrame como uma tabela temporária → atribuir o nome da tabela.

```jsx
df.createOrReplaceTempView(”tabela_temporaria”)
```

→ Executando uma consulta SQL → passar a consulta SQL como uma string.

```jsx
resultado = sqlContext.sql(”SELECT coluna1, coluna2 FROM tabela_temporaria WHERE coluna3 > 10”)
```

→ Exibindo o resultado

```jsx
resultado.show()
```

→ Encerrando a SparkSession

```jsx
spark.stop()
```

O SQLContext fornece uma interface flexível para consultas e seleções de dados usando a sintaxe SQL padrão. 

Permite a execução de operações complexas em dados estruturados usando as funcionalidades do Spark SQL.

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Qual método é usado para ordenar um DataFrame no Apache Spark?

A) filter()

**B) orderBy()**

C) select()

D) groupBy()

E) agg()

2 - Qual método é usado para calcular estatísticas agregadas em um DataFrame no Apache Spark?

A) groupBy()

B) select()

**C) agg()**

D) orderBy()

E) select()

3 - Qual método é usado para agrupar dados em um DataFrame no Apache Spark?

A) filter()

B) select()
**C) groupBy()**

D) orderBy()

E) agg()

4 - Qual método do Apache Spark é usado para selecionar colunas específicas de um DataFrame?

A) orderBy()
**B) select()**

C) groupBy()
D) agg()
E) filter()

5- Qual operação é usada para filtrar linhas de um DataFrame no Apache Spark?

A) orderBy()

B) agg()
C) groupBy()
**D) filter()**

E) select()