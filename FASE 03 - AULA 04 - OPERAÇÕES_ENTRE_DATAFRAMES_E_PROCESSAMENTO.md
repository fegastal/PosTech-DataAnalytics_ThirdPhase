# FASE 03 - AULA 04 - OPERAÇÕES ENTRE DATAFRAMES E ARMAZENAMENTO

Anotações sobre a quarta aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=307799&c=8729&sesskey=mp0PcE8JII](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337984&amp;sesskey=Wfd1uQJe6L)

Temas abordados:

- Aprendemos as principais operações, como filtragem, transformação, agregação e junção de dados, de forma distribuída e otimizada pelo Spark.
- Foram aplicadas práticas com as linguagens Spark e Python, amplamente utilizadas no ecossistema do Spark, permitindo a aplicação de operações avançadas em grandes volumes de dados.
- Diferenças entre RDD, DataFrame e DataSet.

---

## Parte 1 | APIS SPARK RDD

RDD significa Conjuntos de Dados Distribuídos Resilientes (Resilient Distributed Dataset). É uma coleção de registros de partição em que **só é possível a leitura**. 

O **RDD é a estrutura de dados fundamental do Spark** e permite que especialistas em programação executem cálculos na memória em grandes grupos de maneira tolerante a falhas.

Nos APIs do Spark Dataframe, ao contrário de um RDD, os **dados são organizados em colunas nomeadas**. Como, por exemplo, uma tabela em um *banco de dados relacional*; É uma *coleção imutável de dados distribuídos*.

O DataFrame no Spark permite que especialistas em desenvolvimento possam **impor uma estrutura em uma coleção distribuída de dados, permitindo abstração de nível superior**.

Nas APIs do conjunto de dados Spark (DataSets), o conjunto de dados no Apache são uma extensão da API DataFrame, que fornece uma interface de **programação orientada a objetos** e com **segurança de tipo**.

O conjunto de dados aproveita o **otimizador Catalyst** do Spark expondo expressões e campos de dados ao indivíduo planejador de consultas.

---

**RDD x DATAFRAME x DATASET**

→ RDD é uma coleção distribuída de elementos de dado espalhados por muitas máquinas no cluster. Lembrando que RDDs são um conjunto de objetos Java ou Scala que representam dados.

→ DataFrame é uma coleção distribuída de dados organizados em colunas nomeadas. É conceitualmente igual a uma tabela em um banco de dados relacional.

→ DataSet é uma extensão da API DataFrame que fornece a funcionalidade de interface de programação orientada a objetos e segura para tipos de dados da API RDD, benefícios de desempenho do otimizador de consulta Catalyst e mecanismo de armazenamento fora da pilha de uma API DataFrame.

---

**FORMATO DE DADOS**

→ RDD pode processar de maneira mais fácil e eficiente dados estruturados e não estruturados. Como o DataFrame e o DataSets, o RDDs não infere no esquema dos dados ingeridos e exige que o usuário os especifique.

→ O DataFrame funciona apenas em dados estruturados e semiestruturados, ele organiza os dados na coluna nomeada. Permitem que o Spark gerencie o esquema.

→ O DataSet também processa eficientemente dados estruturados e não estruturados. Ele representa dados na forma de objetos de linha da JVM ou uma coleção de objetos de linha que é representada em formas de tabela através de codificadores.

---

**API DA FONTE DE DADOS**

Permite que um RDD possa vir de qualquer fonte de dados, como arquivo de texto, banco de dados via JDBC etc, e manipular facilmente dados sem estrutura predefinida.

Para o DataFrame, a API da fonte de dados permite o processamento de dados em diferentes formatos (AVRO, CSV, JSON e sist de armazenamento HDFS, tabelas HIVE, MySQL).

A API do conjunto de dados do Spark também suporta dados de diferentes fontes no DataSet.

---

**IMUTABILIDADE E INTEROPERABILIDADE**

RDDs contêm a coleção de registros que são particionados.

A unidade básica de paralelismo em um RDD é chamada de partição. Cada participação é uma divisão lógica de dados que é imutável e criada através de alguma transformação nas partições existentes, sendo que a imutabilidade ajuda a obter consistência nos cálculos.

Podemos passa do RDD para o DataFrame (se o RDD estiver no formato tabular) pelo método toDF() ou podemos fazer o inverso pelo método .rdd. Aprenda várias APIs de tranformações e ações de RDD com exemplos.

Após a transformação no DataFrame, não é possível regenerar um objeto de domínio. Por exemplo, se você gerar testDF a partir de testRDD não poderá recuperar o RDD original da classe de teste.

O DataSet supera a limitação do DataFrame para regenerar o RDD do Dataframe.

Os conjuntos de dados permitem converter seus RDD e DataFrames existentes em conjuntos de dados.

---

**USO DE EFICIÊNCIA / MEMÓRIA**

No RDD, a eficiência diminui quando a serialização é realizada individualmente em um objeto Java e Scala que levam muito tempo.

No DataFrame, o uso de memória heap desativada para serialização reduz a sobrecarga. Ele gera código de bytes dinamicamente para que muitas operações possam ser executadas nesses dados serializados. Não há necessidade de desserialização para pequenas operações.

Já o DataSet, permite executar uma operação em dados serializados e melhorar o uso da memória. Assim, ele possibilita o acesso sob demanda ao atributo individual sem desserializar o objeto inteiro.

---

**SUPORTE À LINGUAGEM DE PROGRAMAÇÃO**

APIs RDD estão disponíveis em Java, Scala, Python e R. Portanto, esse recurso fornece flexibilidade a especialistas em desenvolvimento.

O DataFrame também possui APIs em diferentes linguagens, como Java, Python, Scala e R.

Para o DataSet, conjuntos de dados estão disponíveis apenas no Scala e Java. O Spark versão 2.1.1 não suporta Python e R.

---

**AGREGAÇÃO**

API RDD é mais lenta para executar operações simples de agrupamento e agregação;

API DataFrame é fácil de usar, mais rápida para análise exploratória, criando estatísticas agregadas em grandes conjuntos de dados;

API DataSet, no conjunto de dados, é mais rápido executar a operação de agregação em diversos conjuntos de dados.

---

## Parte 2 | ENTENDENDO NA PRÁTICA COMO É O APACHE SPARK

**1 - Criar PySpark RDD**

Primeiro, vamos criar um RDD passando o objeto de lista do Python para **sparkContext.parallelize()**. Precisaríamos deste RDD para todos os nossos exemplos a seguir.

No PySpark, quando você tem dados em uma lista, significa que você tem uma coleção de dados na memória do driver PySpark ao criar um RDD e essa coleção será paralelizada.

```jsx
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName('Tutorial).getOrCreate()
dept = [("Finance",10),("Marketing",20),("Sales",30),("IT",40)]
rdd = spark.sparkContext.parallelize(dept)
```

**2 - PySpark RDD em DataFrame**

A conversão do PySpark RDD para DataFrame pode ser feita usando toDF(), createDataFrame(). Explicaremos esses dois métodos:

**2.1. - Usando a função [rdd.to](http://rdd.to)DF()** → pode ser usada para converter RDD em DataFrame:

```jsx
df = rdd.toDF()
df.printSchema()
df.show(truncate=False)
```

Por padrão, toDF() cria nomes de coluna como “_1” e “_2”. Esse snippet produz o esquema a seguir:

root
|-- _1: string (nullable = true)
|-- _2: long (nullable = true)

+---------+---+
|_1       |_2 |
+---------+---+
|Finance  |10 |
|Marketing|20 |
|Sales    |30 |
|IT       |40 |
+---------+---+

toDF() tem outra assinatura que usa argumentos para definir os nomes das colunas, conforme é possível observar a seguir:

```jsx
deptColumns = ["dept_name","dept_id"]
df2 = rdd.toDF(deptColumns)
df2.printSchema()
df2.show(truncate=False)
```

Segue a saída do esquema:

```jsx
deptDF = spark.createDataFrame(rdd, schema = deptColumns)
deptDF.printSchema()
deptDF.show(truncate=False)
```

**2.2. Usando a função createDataFrame() do PySpark** → é um método para criar DataFrame e leva o RDD como um argumento dentro da função.

```jsx
from pyspark.sql.types import StructType,StructField, StringType
deptSchema = StructType([
StructField('dept_name', StringType(), True),
StructField('dept_id', StringType(), True)
])
deptDF1 = spark.createDataFrame(rdd, schema = deptSchema)
deptDF1.printSchema()
deptDF1.show(truncate=False)
```

Isso produz a mesma saída apresentada.

**2.3. Usando createDataFrame() com esquema StructType:**

Quando você infere o esquema, por padrão, o tipo de dados das colunas é derivado dos dados e definido como nullable e true para todas as colunas.

Podemos alterar esse comportamento fornecendo o esquema usando StructType - em que podemos especificar um nome de coluna, tipo de dados e anulável para cada campo / coluna.

```jsx
rom pyspark.sql.types import StructType,StructField, StringType
deptSchema = StructType([
StructField('dept_name', StringType(), True),
StructField('dept_id', StringType(), True)
])
deptDF1 = spark.createDataFrame(rdd, schema = deptSchema)
deptDF1.printSchema()
deptDF1.show(truncate=False)
```

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Qual método do Apache Spark é utilizado para carregar um arquivo CSV em um DataFrame?

A) readFromCSV()

B) loadCSV()

C) loadFromCSV()
**D) readCSV()**

E) importCSV()

2 - Qual método do DataFrame é utilizado para filtrar linhas com base em uma condição no Apache Spark?

**A) filter()**
B) select()
C) where()
****D) sort()
E) groupBy()

3 - Qual é a função utilizada para verificar a quantidade de linhas em um DataFrame no Apache Spark?

A) shape()
B) length()
C) rows()
D) size()
**E) count()**

4 - Qual operação é utilizada para juntar dois DataFrames com base em colunas comuns no Apache Spark?

**A) join()**

B) append()
C) union()
****D) intersect()
E) merge()

5- Qual é a função utilizada para salvar um DataFrame em um formato específico no Apache Spark?

A) save()

B) export()
C) persist()

**D) write()**
E) store()