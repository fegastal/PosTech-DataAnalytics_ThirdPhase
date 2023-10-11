# FASE 03 - AULA 07 - REALIZAÇÃO DE CONSULTAS COM BIGQUERY

Anotações sobre a sétima aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337986&amp;sesskey=aUi3fmwArb](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=338014&c=9543&sesskey=s1k1poBKHM)

Temas abordados:

- Google Cloud Platform
- O que é BigQuery?
- Como usar a infraestrutura do Google Cloud para consulta e processamento avançado de **grandes volumes de dados** dentro da nuvem?

---

## Introdução

Google BigQuery é uma poderosa ferramenta de análise de dados em escala empresarial, que permite explorar e extrair insights valiosos de grandes conjuntos de dados.

Vamos nos aprofundar em consultas SQL (Structured Query Language) e aprender como aplicar essas habilidades ao BigQuery. Vamos explorar como pode ser utilizado para realizar consultas avançadas em grandes volumes de dados no Google BigQuery, desde a criação de tabelas e carregamento de dados até a execução de consultas complexas.

Bom para iniciantes em SQL e profissionais experientes também. 😊

---

## Parte 1 | GOOGLE BIGQUERY

Foi projetado como um Data Warehouse “nativo da nuvem”. Foi criado para atender às necessidades de organizações orientadas a dados em um primeiro mundo em nuvem.

É o armazenamento de dados em nuvem sem servidor, altamente escalonável e econômico do Google Cloud Platform. Permite consultas super-rápidas em escala de pentabytes usando o poder de processamento da infraestrutura do Google.

Como não há infraestrutura para os clientes gerenciarem, eles podem se concentrar em **descobrir insights significativos usando SQL familiar**, sem a necessidade de um administrador de banco de dados. Também é econômico porque eles pagam apenas pelo **processamento e armazenamento** que usam.

![Untitled](FASE%2003%20-%20AULA%2007%20-%20REALIZAC%CC%A7A%CC%83O%20DE%20CONSULTAS%20COM%20%2064e15ea9677a414ea22a273e339a8be9/Untitled.png)

O BigQuery está dentro de um grupo de soluções com foco em Big Data, é possível notar que dentro do portfólio de soluções existem diversos produtos para finalidades específicas.

---

### Parte 2 - **ENTENDENDO MELHOR O GOOGLE BIGQUERY E SUAS INTEGRAÇÕES**

O BigQuery é compatível com várias maneiras de receber dados no armazenamento gerenciado. O método de ingestão específico depende da origem dos dados.

Exemplo: algumas fontes de dados no GCP, como **Cloud Logging e Google Analytics**, oferecem suporte a exportações diretas para o BigQuery. Basta ativar o recurso, fornecer o acesso e os dados começam a ser enviados automaticamente para o Google BigQuery na frequência desejada.

Já o **BigQuery Data Transfer Service** permite a transferência de dados para o BigQuery de aplicativos **Google SaaS** (por exemplo *Google Ads e Cloud Storage*), **Amazon S3** e outros **data warehouses (Teradata, Redshift)**.

Os dados de streaming, como registros ou dados de dispositivos IoT, podem ser gravados no BigQuery usando pipelines do Cloud Dataflow, jobs do Cloud DataProc ou **diretamente usando a API de ingestão de stream do BigQuery**.

---

### Parte 3 - ACESSANDO A INTERFACE DO GOOGLE BIGQUERY

**A | CADASTRO**

1 → Get Started for Free [https://cloud.google.com/](https://cloud.google.com/)

2 → Login com a conta Google

3 → Página de boas-vindas → Start my free trial

4 → Redirecionamento para o console da GCP para criar projetos, configurar recursos e acessar os serviços da plataforma.

5 → Revisar as configurações de faturamento e limites de uso para garantir que esteja ciente de quaisquer encargos ou restrições no Painel do Console da GCP.

**B | NAVEGAR ATÉ O RECURSO DO BIGQUERY**

![Untitled](FASE%2003%20-%20AULA%2007%20-%20REALIZAC%CC%A7A%CC%83O%20DE%20CONSULTAS%20COM%20%2064e15ea9677a414ea22a273e339a8be9/Untitled%201.png)

Na tela inicial, já temos a opção de visualizar alguns conjuntos de dados disponíveis por padrão e também a opção de levar seus dados para o BigQuery através dos importadores de Arquivo Local, Google Drive ou Google Cloud Storage.

---

### Parte 4 - EXPLORANDO A INTERFACE DO GOOGLE BIGQUERY

Após criar um projeto, vamos entender melhor como funciona a interface do BigQuery. Após criar o projeto, ele aparecerá para mim no canto superior esquerdo. (1)

Logo abaixo, terá uma lista de projeto fixos do BigQuery, entre esses, o “bigquery-public-data”. (2)

A seta à esquerda do nome “bigquery-public-data” nos permite expandir a lista de todas as bases disponíveis na logo abaixo.

![Untitled](FASE%2003%20-%20AULA%2007%20-%20REALIZAC%CC%A7A%CC%83O%20DE%20CONSULTAS%20COM%20%2064e15ea9677a414ea22a273e339a8be9/Untitled%202.png)

Na imagem, cada botão possui uma finalidade específica, então:

1. Navegar pela lista de projetos disponíveis na sua conta.
2. Visualizar a lista de conjuntos de dados disponíveis.
3. Local onde você escreve sua consulta SQL, para escrever e executar consultas.
4. Onde você consegue visualizar seus resultados de consultas executadas.
5. Salvar seus resultados de execução (CSV, JSON, Google Sheets).
6. Exploração de dados com Google Sheets, Looker Studio, Geo Viz e Google Colab.
7. Executar a consulta SQL que você escreveu no console.
8. Visualizar as informações técnicas de execução do resultado da consulta.

---

### Parte 5 - EXPLORANDO CONJUNTOS DE DADOS PÚBLICOS NO GOOGLE BIGQUERY

Agora que acessamos o Google BigQuery, vamos entender melhor como funcionam os objetos disponíveis e seus conjuntos de dados públicos → são basicamente bases de dados disponibilizados pela equipe do Google Cloud para fins de testes e experimentação. Dessa forma, novos analistas de dados conseguem ter um ambiente para estudo longo após a realização do cadastro.

![Untitled](FASE%2003%20-%20AULA%2007%20-%20REALIZAC%CC%A7A%CC%83O%20DE%20CONSULTAS%20COM%20%2064e15ea9677a414ea22a273e339a8be9/Untitled%203.png)

Aqui acima, por exemplo, se procurarmos pela palavra “census”, a pesquisa retorna esses resultados.

---

### Parte 6 - ENTENDENDO CONSULTAS SQL NO GOOGLE BIGQUERY

SQL é uma das linguagens mais reconhecidas no mundo todo para extração, processamento e manipulação de dados. Ela é uma importante ferramenta de trabalho e pode trazer bastante autonomia e produtividade para os trabalhos que envolvam análise de dados.

É uma linguagem que precisa de um compilador (ou interface) para ser executado. Nesse caso, usamos o BigQuery como camada de acesso aos dados.

Dentro de uma consulta SQL, existem várias cláusulas e comandos que podem ser usados para personalizar e refinar os resultados. Abaixo estão os principais comandos e cláusulas utilizados em uma consulta SQL:

1 | SELECT → especificar as colunas que você deseja selecionar na consulta. Pode selecionar colunas específicas separando-as por vírgulas ou usar o * para selecionar todas as colunas da tabela.

2 | FROM → especificar a tabela a partir das quais você deseja recuperar os dados. Permite que você especifique a fonte dos dados para a consulta.

3 | WHERE → filtrar os resultados com base em uma condição específica. Pode usar operadores de comparação (como igual a, maior que, menor que) e operadores lógicos (como AND, OR, NOT) para construir condições complexas.

4 | GROUP BY → agrupar os resultados com base em uma ou mais colunas. Permite que faça agregações como contar, somar ou encontrar valores máximos / mínimos, dentro de cada grupo usando funções de agregação, como COUNT, SUM, MAX, MIN.

5 | HAVING → aplicada em conjunto com a cláusula GROUP BY, para filtrar grupos com base em condições específicas. Funciona de maneira semelhante à cláusula WHERE, mas opera nos resultados após a execução da cláusula GROUP BY.

6 | ORDER BY → utilizada pra classificar os resultados em uma determinada ordem. Pode organizar os resultados em ordem ascendente (ASC) ou descendente (DESC) com base em uma ou mais colunas.

7 | JOIN → para combinar registros de duas ou mais tabelas com base em uma condição de correspondência entre elas. Existem diferentes tipos de junções, como INNER, JOIN, LEFT JOIN, RIGHT JOIN e FULL JOIN, que determinam como os registros são combinados.

8 | DISTINCT → utilizado para retornar apenas valores distintos das colunas selecionadas. Ele elimina duplicatas nos resultados da consulta.

Esses são os principais comandos e cláusulas em uma consulta SQL. Combinando-os de maneira adequada, podemos personalizar e refinar os resultados de acordo com as necessidades específicas. Vamos experimentá-los juntos? 😃

---

### Parte 7 - ESCREVENDO A ESTRUTURA DE UMA CONSULTA SQL

Agora vamos usar o poder do BigQuery para processar os dados de maneira massiva e otimizada.

**1 | CONSULTA SQL SEM AGREGAÇÃO:**

```jsx
SELECT [nome_da_coluna_1], [nome_da_coluna_2], [nome_da_coluna_3]
FROM [nome_do_esquema].[nome_da_tabela]
```

**2 | CONSULTA SQL SEM AGREGAÇÃO E COM CONDIÇÃO DE FILTRO E ORDENAÇÃO DE RESULTADO POR CAMPO:**

```jsx
SELECT [nome_da_coluna_1], [nome_da_coluna_2], [nome_da_coluna_3]
FROM [nome_do_esquema].[nome_da_tabela]
WHERE [condição]
ORDER BY [campo_de_ordenacao]
```

**3 | CONSULTA SQL COM AGREGAÇÃO DE SOMA POR 3 CAMPOS:**

```jsx
SELECT [nome_da_coluna_1], [nome_da_coluna_2], [nome_da_coluna_3], SUM([nome_do_campo] AS [nome_do_campo]
FROM [nome_do_esquema].[nome_da_tabela]
GROUP BY [nome_da_coluna_1], [nome_da_coluna_2], [nome_da_coluna_3]
```

4 **| CONSULTA SQL COM AGREGAÇÃO DE SOMA POR 3 CAMPOS E ORDENAÇÃO DE RESULTADO POR CAMPO:**

```jsx
SELECT [nome_da_coluna_1], [nome_da_coluna_2], [nome_da_coluna_3], SUM([nome_do_campo] AS [nome_do_campo]
FROM [nome_do_esquema].[nome_da_tabela]
GROUP BY [nome_da_coluna_1], [nome_da_coluna_2], [nome_da_coluna_3]
ORDER BY [campo_de_ordenacao]
```

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

**1 - Como os dados são armazenados no Google BigQuery?**

A) Em colunas otimizadas em um formato colunar chamado Capacitor.

~~B) Em um formato colunar chamado Capacitor que permite consultas rápidas e eficientes em grandes conjuntos de dados.~~

C) Em bancos de dados relacionais tradicionais.
D) Em tabelas estruturadas em um formato de arquivo específico.

E) Em um sistema de arquivos distribuído chamado.

2 - Qual é a finalidade do uso de partições e clustering no Google BigQuery?

A) Garantir a segurança dos dados.
B) Facilitar a integração com outras ferramentas de análise de dados.
**C) Melhorar o desempenho das consultas.**
D) Reduzir a latência das consultas.
E) Economizar custos de armazenamento.

3 - Qual das seguintes opções descreve corretamente o Google BigQuery?

**A) Um serviço de armazenamento e processamento de dados totalmente gerenciado do Google Cloud.**
B) Um banco de dados relacional com suporte para transações ACID.
C) Um banco de dados NoSQL baseado em documentos.
D) Um serviço de armazenamento em nuvem para arquivos de texto simples.
E) Um serviço de análise de dados em larga escala que permite consultas rápidas e eficientes em grandes conjuntos de dados.

4 - Qual linguagem de consulta é usada para interagir com o Google BigQuery?

A) R.

B) JavaScript.
C) Python.
D) Scala.
**E) SQL.**

5 - Qual das seguintes opções é usada para consultar dados no Google BigQuery?

**A) ‘SELECT’.**

B) ‘DROP DATABASE’.
C) ‘INSERT’.

D) ‘UPDATE’.
E) Todas as opções anteriores.

---