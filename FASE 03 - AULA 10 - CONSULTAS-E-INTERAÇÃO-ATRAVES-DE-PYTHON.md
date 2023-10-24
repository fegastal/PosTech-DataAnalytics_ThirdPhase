# FASE 03 - AULA 10 - CONSULTAS E INTERAÇÃO ATRAVÉS DE PYTHON

Anotações sobre a décima aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337986&amp;sesskey=aUi3fmwArb](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=338017&amp;sesskey=aitTcWBLwg)

Temas abordados:

- Veremos mais sobre o Google Colab e como esta plataforma de ciência de dados proporciona maiores possibilidades de uso dos dados quando combinada com o poder de processamento do Google BigQuery.

---

## Introdução

→ Plataforma baseada na nuvem desenvolvida pelo Google onde é possível escrever, executar e colaborar em código Python. 

→ Ferramenta popular para aprendizado de máquina, análise de dados e desenvolvimento de projetos baseados em Python.

1 | **Ambiente de notebook** → Interativo, que permite os usuários escrever e executar códigos Python. Os notebooks são compostos por células, onde *cada célula pode conter código, texto ou visualizações*. Nele, é possível criar *novas células, editar as existentes e executá-las individualmente*.

2 | **Baseado em Jupyter** → Oferece uma experiência semelhante ao Jupyter Notebook local. Isso permite que as pessoas escrevam códigos, visualizem os resultados e documentem seus projetos em um único ambiente interativo.

![Untitled](FASE%2003%20-%20AULA%2010%20-%20CONSULTAS%20E%20INTERAC%CC%A7A%CC%83O%20ATRAVE%203ce48a8c961b4371907cf4facacdd8b9/Untitled.png)

3 | **Acesso à GPU e TPU** → uma das principais vantagens é a capacidade de acessar recursos de processamento de alto desempenho, como Unidades de Processamento Gráfico (GPUs) e Unidades de Processamento Tensorial (TPUs). É particularmente útil para tarefas de aprendizado de máquina e processamento de dados intensivos.

4 | **Armazenamento e importação de dados** → permite importar dados de várias fontes, como Google Drive, Github e até mesmo diretamente do computador local do usuário. Os dados podem ser armazenados temporariamente no ambiente de execução do Colab ou carregados para a memória RAM para análise e processamento.

![Untitled](FASE%2003%20-%20AULA%2010%20-%20CONSULTAS%20E%20INTERAC%CC%A7A%CC%83O%20ATRAVE%203ce48a8c961b4371907cf4facacdd8b9/Untitled%201.png)

5 | **Bibliotecas e pacotes pré-instalados** → o Colab já vem pré-instalado com muitas habilidades e pacotes populares, como Numpy, Pandas, Matplotlib e TensorFlow, o que facilita a análise de dados e o desenvolvimento de modelos de aprendizado de máquina. Além disso, é possível instalar facilmente outras bibliotecas usando o gerenciador de pacotes Python, o pip.

6 | **Colaboração em tempo real** → permite que várias pessoas colaborem em um único notebook ao mesmo tempo. Você pode compartilhar seus notebooks com outras pessoas por meio de um link e trabalhar em conjunto em projetos de maneira síncrona. Isso facilita a colaboração em equipes de desenvolvimento e o compartilhamento de conhecimento.

7 | **Integração com outros serviços do Google** → integrado ao ecossistema de serviços do Google. Significa que é possível acessar facilmente o armazenamento do Google Drive, importar conjuntos de dados do Google Sheets, visualizar gráficos usando o Google Charts e muito mais.

O Google Colab oferece uma maneira conveniente e acessível de desenvolver e executar projetos baseados em Python na nuvem. 

Tem natureza colaborativa, recursos de hardware poderosos e integração com outros serviços do Google que o tornam uma escolha popular entre estudantes, pessoas que realizam pesquisas e especialistas em desenvolvimento.

---

## Parte 1 | COMO CONECTAR O GOOGLE BIGQUERY AO AMBIENTE GOOGLE COLAB?

### **1 | Conectar o BigQuery ao Google Colab pela interface do BigQuery:**

1 - Abra o Google Colab no navegador

2 - Na barra de menu superior, clique em “Inserir” e, em seguida, em “Código”

3 - Será criada uma célula de código vazia → digite o código abaixo:

```jsx
!pip install google-cloud-bigquery
from google.cloud import bigquery
```

4 - Acesse o Console do Google Cloud no site do console → [https://console.cloud.google.com/](https://console.cloud.google.com/)

5 - No canto superior direito, clique no ícone de seleção do projeto e selecione o projeto do Google Cloud em que você está trabalhando

6 - No painel de navegação à esquerda, clique em “BigQuery” para abrir a interface do BigQuery

7 - Na interface do BigQuery, clique no nome do projeto no canto superior esquerdo e selecione o projeto que corresponde ao projeto do Google Cloud que você selecionou anteriormente no Google Colab

8 - Agora, obter as credenciais de autenticação para conectar o BigQuery ao Colab. Para isso, clique no ícone de chave inglesa no canto superior direito da página e selecione “Configurações”

9 - Na guia “Credenciais”, role para baixo até “Credenciais da API” e clique em “Criar Credenciais”

10 - Selecione “Chave da conta de serviço” na lista suspensa

11 - Na seção “Painéis”, selecione “BigQuery” > “BigQuery Admin” para conceder permissões de adm

12 - Clique em “Continuar” e, em seguida, “Criar sem opção de fornecer o consentimento do usuário”

13 - Será feito o download de um arquivo JSON contendo suas credenciais. Guarde-o em um local seguro

14 - Volte ao Google Colab e clique em “Arquivo” > “Carregar” e carregue o arquivo JSON de credenciais que você baixou

15 - Para criar uma conexão com o BigQuery, adicione o seguinte código em uma célula de código no Colab:

```jsx
rom google.colab import auth
auth.authenticate_user()
```

16 - Execute a célula de código e siga as instruções para fazer login na sua conta do Google

17 - Após autenticar, pode usar o BigQuery no Colab usando a biblioteca ‘google.cloud.bigquery’

### **2 | Conectar o BigQuery ao Google Colab via código Python**

1 | Abra o Colab no navegador

2 | Na barra de menu superior, clique em “Inserir” e, em seguida, em “Código”

3 | Será criada uma célula de código vazia. Digite:

```jsx
!pip install google-cloud-bigquery
from google.cloud import bigquery
```

4 | Para autenticar a conexão com o BigQuery no Colab, adicione o seguinte código em uma célula de código:

```jsx
from google.colab import auth
auth.authenticate_user()
```

5 | Execute a célula de código e siga as instruções para fazer login na sua conta do Google

6 | Depois de autenticar, você pode usar o BigQuery no Colab usando a biblioteca ‘google.cloud.bigquery’. Por exemplo, você pode executar consultas SQL e obter resultados diretamente no Colab

Essas são maneiras de conectar o BigQuery ao Google Colab. A primeira opção permite que você use a interface do BigQuery para executar consultas, enquanto a segunda opção permite que você execute consultas diretamente usando código Python no Colab.

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Qual comando Python é usado para executar consultas SQL em um banco de dados?

**A) execute()**

B) query()

C) connect()
****D) pull()

E) fetch()

2 - Qual biblioteca Python é frequentemente usada para interagir com bancos de dados relacionais?

**A) SQLAlchemy**
B) Matplotlib
****C) Searbon
D) NumPy
E) Pandas

3 - Qual módulo Python é usado para se conectar a um banco de dados e executar consultas SQL?

A) xml
****B) os
C) pymysql
****D) json
**E) sqlite3**

4 - Qual método Python é usado para obter os resultados de uma consulta SQL executada em um banco de dados?

A) commit()

B) get()

C) execute()

D) fetch()

**E) fetchall()**

5 - Qual biblioteca Python permite trabalhar com bancos de dados NoSQL, como MongoDB?

A) Spark

B) Django
C) Redis

D) Flask
**E) PyMongo**

---