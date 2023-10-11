# FASE 03 - AULA 02 - OPERAÇÕES BÁSICAS NO APACHE SPARK

Anotações sobre a segunda aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=307799&c=8729&sesskey=mp0PcE8JII](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337982&c=9543&sesskey=7rr89OBC9S)

Temas abordados:

- Como realizar operações básicas de transformação e manipulação de dados em escala;
- Leitura e gravação de dados até aplicação de filtros, mapeamento e agregações;
- Uso das linguagens de programação como Scala ou Python, amplamente utilizadas no Spark;
- Criar RDDs (Resilient Distributed Datasets) → estrutura fundamental do Spark;
- Realizar transformações e ações para processar e extrair informações valiosas dos dados;
- Processamento de grande volume de informações de maneira rápida, escalável e eficiente.

---

## Parte 1 | TRANSFORMAÇÕES E AÇÕES

Operações fundamentais para processar e manipular dados distribuídos em **RDDs (Resilient Distributed Datasets)**. 

### Transformações

→ Operações que criam um novo RDD a partir de um RDD existente;

→ São preguiçosas (lazy), o que significa que a execução real da transformação não ocorre imediatamente, apenas quando uma ação é chamada;

→ Transformações são processadas de forma distribuída e podem ser executadas em paralelo em diferentes nós do cluster;

→ São imutáveis, o que significa que não modificam o RDD original, mas criam um novo RDD com as modificações aplicadas;

→ Exemplos:

1 **Map** → aplica uma função a cada elemento do RDD e retorna um novo RDD com os resultados correspondentes;

2 **Filter** → retorna um novo RDD contendo apenas os elementos que satisfazem uma determinada condição;

3 **FlatMap** → similar ao Map, porém cada elemento de entrada pode gerar zero ou mais elementos de saída. Os resultados são achatados em um único RDD.

4 **GroupBy** → agrupa os elementos do RDD com base em uma determina chave e retorna um novo RDD de pares (chave, lista de valores).

5 **ReduceByKey** → agrega os valores de cada chave em um RDD, aplicando uma função de redução.

6 **SortBy** → ordena os elementos do RDD com base em uma chave específica.

7 **Join** → combina dois RDDs com base em chaves correspondentes, gerando um novo RDD contendo os pares combinados.

8 **Union** → une dois RDDs em um único RDD, preservando todos os elementos.

9 **Distinct** → retorna um novo RDD com elementos únicos, removendo duplicatas.

→ Exemplos práticos:

1 - Importando módulos necessários:

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col
```

2 - Criando uma sessão Spark:

```python
spark = SparkSession.builder.appName("Exemplos PySpark").getOrCreate()

# Carregar dados de um arquivo CSV
df = spark.read.csv("/arquivo_teste.csv", header=True, inferSchema=True)

# Exibir o schema do DataFrame
df.printSchema()

# Selecionar colunas específicas
df_selected = df.select("coluna1", "coluna2")

# Filtrar registros com base em uma condição
df_filtered = df.filter(col("coluna3") > 100)

# Adicionar uma nova coluna calculada
df_with_new_column = df.withColumn("nova_coluna", col("coluna1") * 2)

# Renomear uma coluna
df_renamed_column = df.withColumnRenamed("coluna1", "novo_nome_coluna")
```

### Ações

→ São operações que retornam resultados ou gravam dados;

→ Desencadeiam a execução das transformações anteriores no RDD, iniciando o processamento real dos dados;

→ Ações podem retornar resultados para o programa driver ou gravar dados em sistemas externos;

→ São executadas de forma distribuída, envolvendo os nós do cluster para processar os dados;

→ Exemplos: 

1 **Count** → retorna o número de elementos no RDD.

2 **Collect** → coleta todos os elementos do RDD e os retorna como uma lista no programa driver. Útil para RDDs pequenos, pois todos os dados são retornados para a máquina local.

3 **First** → retorna o primeiro elemento do RDD.

4 **Take** → retorna os primeiros elementos do RDD como uma lista.

5 **Reduce** → aplica uma função de redução a todos os elementos do RDD e retorna o resultado final.

6 **Foreach** → aplica uma função a cada elemento do RDD. É útil para executar operações de efeito colateral, como gravar em um banco de dados ou escrever em um sistema de arquivos.

7 **SaveAsTextFile** → grava os elementos do RDD em um arquivo de texto no sistema de arquivos.

8 **CountByValue** → conta o número de ocorrências de cada valor no RDD e retorna os resultados como um mapa (chave, contagem).

9 **Sum** → retorna a soma de todos os elementos numéricos no RDD.

→ Exemplos práticos:

1 - Importando os módulos necessários:

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col
```

2 - Criando uma sessão Spark:

```python
spark = SparkSession.builder.appName("Exemplos PySpark").getOrCreate()

# Carregar dados de um arquivo CSV
df = spark.read.csv("/arquivo_teste.csv", header=True, inferSchema=True)
```

3 - Exemplo 2: executando ações em um DataFrame

```python
# Contar o número total de registros
count = df.count()
print("Número total de registros: ", count)

# Exibir uma amostra dos dados
df_sample = df.sample(fraction=0.1, seed=42)
df_sample.show()

# Calcular a média de uma coluna
average = df.select("coluna1").groupBy().avg().collect()[0][0]
print("Média da coluna1: ", average)

# Salvar o DataFrame em um arquivo CSV
df.write.csv("/arquivo_teste.csv", header=True)
```

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Qual o principal desafio ao disponibilizar uma base de dados em uma infraestrutura de nuvem?

A) Dificuldade em escalar horizontalmente.

**B) Dependência de fornecedores de nuvem.**

C) Falta de segurança dos dados.

D) Custos com migração de infraestrutura.

E) Restrições de largura de banda.

2 - Qual das seguintes opções é uma plataforma de infraestrutura de nuvem popular para disponibilização de base de dados?

A) Microsoft Azure.

B) Alibaba Cloud.

**C) Todas as anteriores.**

D) Amazon Web Services (AWS).

E) Google Cloud Platform (GCP).

3 - Qual das seguintes opções descreve corretamente a disponibilização de uma base de dados em uma infraestrutura de nuvem?

**A) Utilizar um serviço de base de dados em nuvem, como o Amazon RDS.**

B) Hospedar a base de dados em servidores físicos no local.

C) Utilizar uma biblioteca de processamento de dados como o Apache Spark.

D) Utilizar uma plataforma de Big Data como o Apache Hadoop.

E) Utilizar um serviço de armazenamento em nuvem, como o Google Cloud Storage.

4 - Quais são os benefícios da disponibilização de uma base de dados em uma infraestrutura de nuvem?

A) Menor custo de infraestrutura.

**B) Todas as anteriores.**

C) Maior segurança dos dados.

D) Maior escalabilidade e flexibilidade.

E) Maior velocidade no processamento de grandes volumes.

5- Qual é a principal vantagem de utilizar uma infraestrutura de nuvem para a disponibilização de base de dados?

A) Melhor desempenho devido à proximidade física com os usuários.

B) Menor risco de perda de dados.

**C) Redução da carga operacional e manutenção da infraestrutura.**

D) Maior controle sobre o hardware utilizado.

E) Menor tempo de processamento de consultas.