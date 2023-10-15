# FASE 03 - AULA 09 - INTERAÇÕES COM FERRAMENTAS EXTERNAS

Anotações sobre a nona aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337986&amp;sesskey=aUi3fmwArb](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=338016&c=9543&sesskey=43J8417eqQ)

Temas abordados:

- Veremos como usar o **BigQuery** como um repositório de dados eficiente e utilizamos ele como **fonte de dados** para conectar em outras ferramentas como o Tableau (ferramenta de visualização de dados líder nesse segmento);
- **Google Colab** → solução do Google para trabalhar com notebooks Python e desenvolver modelos e algoritmos de Machine Learning e Inteligência Artificial.

---

## Introdução

→ Integração de ferramentas externas: Google Colab + Tableau + Google BigQuery

→ Como conectar-se e utilizar essas poderosas ferramentas em conjunto para realizar análises de dados avançadas e visualizações impactantes?

→ No mundo atual, profissionais de dados e analistas precisam lidar com conjuntos de dados cada vez maiores e complexos. Felizmente, existem várias ferramentas disponíveis que podem nos ajudar nessa tarefa.

→ Google Colab é um ambiente de notebook baseado na nuvem que permite escrever e executar código Python, ideal para explorar e transformar dados.

→ Tableau é uma plataforma de visualização de dados líder no mercado, que permite criar painéis interativos e gráficos impressionantes.

→ No entanto, muitas vezes precisamos trabalhar com grandes volumes de dados armazenados em sistemas distribuídos. É aí que o Google BigQuery entra em cena. É um serviço de armazenamento e análise de dados na nuvem que oferece escalabilidade e velocidade excepcionais. 

→ Ao conectar essas três ferramentas, podemos aproveitar a flexibilidade do Colab, a capacidade de visualização do Tableau e o poder de processamento do BigQuery para realizar análises avançadas de forma mais eficiente.

→ Conexão entre os 3 + importar e exportar dados entre essas ferramentas e como aproveitar os recursos exclusivos de cada uma delas para obter insights valiosos.

---

## Parte 1 | INTRODUÇÃO À CONEXÃO COM FERRAMENTAS EXTERNAS

O BigQuery é um serviço totalmente gerenciado, que permite:

_ **armazenar,** 

_ **consultar** 

_ **e analisar grandes volumes de dados** 

de forma rápida e eficiente.

Escalabilidade e desempenho excepcionais.

Aprender a conectar e utilizar ferramentas externas, como Python e Tableau para a manipulação e visualização de dados, tornando-as valiosas para a análise de dados no contexto do BigQuery.

---

### Parte 2 - CONECTANDO O GOOGLE BIGQUERY NO TABLEAU

O Tableau é compatível nativamente com o Google BigQuery, o que facilita a conexão entre os dois.

1 | **ABRA O TABLEAU DESKTOP** → certifique-se de ter o Tableau Desktop instalado no computador. Você pode fazer o download da versão gratuita de 14 dias no site oficial do Tableau:

[https://www.tableau.com/pt-br/products/desktop](https://www.tableau.com/pt-br/products/desktop)

2 | **TELA INICIAL** → Ao abrir o Tableau Desktop, veremos a tela inicial. Selecione “*Conectar a um Servidor*” no canto superior esquerdo da tela. 

![Untitled](FASE%2003%20-%20AULA%2009%20-%20INTERAC%CC%A7O%CC%83ES%20COM%20FERRAMENTAS%20E%2064e15ea9677a414ea22a273e339a8be9/Untitled.png)

3 | **ESCOLHA O BIGQUERY** → Na janela “Conectar a um Servidor”, você verá uma lista de conexões disponíveis. Localize e selecione “*Google BigQuery*” na lista.

![Untitled](FASE%2003%20-%20AULA%2009%20-%20INTERAC%CC%A7O%CC%83ES%20COM%20FERRAMENTAS%20E%2064e15ea9677a414ea22a273e339a8be9/Untitled%201.png)

4 | **Insira as informações de autenticação**: você precisa fornecer as informações de autenticação para se conectar ao BigQuery. Existem duas opções: “Chave de API” ou “Credenciais do Google”. Selecione a opção de autenticação que melhor se adequa às suas necessidades e forneça as informações correspondentes.

a) *Chave de API* → gerar uma chave de API no Console de APIs e Serviços do Cloud. Siga as instruções para criar uma chave de API e copie a chave para a área designada no Tableau.

b) *Credenciais do Google* → Será solicitado que faça login em sua conta do Google. Após fazer login, o Tableau usará automaticamente suas credenciais para autenticar a conexão.

![Untitled](FASE%2003%20-%20AULA%2009%20-%20INTERAC%CC%A7O%CC%83ES%20COM%20FERRAMENTAS%20E%2064e15ea9677a414ea22a273e339a8be9/Untitled%202.png)

5 | Teste a conexão → para verificar se o Tableau consegue se conectar com sucesso ao BigQuery. Se for bem-sucedida, verá uma mensagem de confirmação:

![Untitled](FASE%2003%20-%20AULA%2009%20-%20INTERAC%CC%A7O%CC%83ES%20COM%20FERRAMENTAS%20E%2064e15ea9677a414ea22a273e339a8be9/Untitled%203.png)

6 | **Acesse seus dados** →após configurar a conexão e testá-la com sucesso, você pode acessar seus dados no BigQuery. O Tableau mostrará uma lista de tabelas e visualizações disponíveis no projeto do Google Cloud que especificou. Selecione as tabelas ou visualizações que deseja usar e clique em “Conectar” para iniciar a análise dos dados.

![Untitled](FASE%2003%20-%20AULA%2009%20-%20INTERAC%CC%A7O%CC%83ES%20COM%20FERRAMENTAS%20E%2064e15ea9677a414ea22a273e339a8be9/Untitled%204.png)

![Untitled](FASE%2003%20-%20AULA%2009%20-%20INTERAC%CC%A7O%CC%83ES%20COM%20FERRAMENTAS%20E%2064e15ea9677a414ea22a273e339a8be9/Untitled%205.png)

Nessa etapa, você pode selecionar o “projeto de faturamento”, o “projeto” e então qual é o “conjunto de dados” desejado para a conexão.

Depois dessa etapa, seguimos com o processo padrão de conexão e importação de dados no Tableau e seguimos com a geração dos insights e análises gráficas. São etapas básicas para conectar o Google BigQuery ao Tableau. Lembre-se de que os procedimentos exatos podem variar dependendo da versão do Tableau e do ambiente em que você está trabalhando. Se encontrar dificuldade, consulte a documentação oficial do Tableau ou entre em contato com o suporte do Tableau para obter assistência adicional. 🙂

---

### Parte 3 - CONECTANDO O BIGQUERY AO GOOGLE COLAB

**1 | CONFIGURAÇÃO INICIAL**

Você precisa autenticar sua conta do Google Cloud para acessar o BigQuery. Para fazer isso, execute o seguinte código no Google Colab:

```jsx
from google.colab import auth
auth.authenticate_user()
```

Isso abrirá uma janela pop-up para autenticação. Faça login com a conta do Google Cloud associada ao seu projeto do BigQuery.

**2 | INSTALAR A BIBLIOTECA DO CLIENTE BIGQUERY NO AMBIENTE DO COLAB**

```jsx
!pip install google-cloud-bigquery
```

**3 | IMPORTAR A BIBLIOTECA DO CLIENTE BIGQUERY**

Agora, importe a biblioteca do cliente BigQuery para poder usar as funcionalidades do BigQuery no Colab:

```jsx
from google.cloud import bigquery
```

**4 | CONFIGURAR O CLIENTE BIGQUERY**

Crie uma instância do cliente BigQuery e configure-a com as credenciais do projeto:

```jsx
project_id = ‘seu-projeto-id’ # Substitua pelo ID do seu projeto no Google Cloud
client = bigquery.Client(project=project_id)
```

**5 | EXECUTAR CONSULTAS NO BIGQUERY**

Agora você pode usar o cliente BigQuery para executar consultas e interagir com seus conjuntos de dados. Exemplo de consulta:

```jsx
query = “””SELECT * FROM seu-projeto-id.seu-dataset-id.sua-tabela-id LIMIT 10”””
query_job = client.query(query)
results = query_job.result()
for row in results:
print(row)
```

Obs: substitua “seu-projeto-id.seu-dataset-id.sua-tabela-id” pelo caminho correto para sua tabela no BigQuery. Ao seguir essas etapas, você poderá conectar o BigQuery ao Colab e começar a explorar e analisar dados usando o poder do BigQuery no ambiente de notebook interativo do Colab.

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Qual das seguintes opções descreve uma ferramenta de Business Intelligence (BI)?

A) Apache Hadoop.

B) Python.

**C) Tableau.**
D) MySQL.

E) Spark.

2 - Qual das seguintes opções é uma linguagem de programação frequentemente utilizada para interagir com bancos de dados?

A) TypeScript / Ruby.
B) Java / .Net.
****C) HTML / CSS.
D) Cobol / C#.
**E) SQL / Python.**

3 - Qual é o objetivo principal de uma ferramenta de BI?

A) Realizar transformações e limpezas nos dados.
****B) Criar modelos de Machine Learning
**C) Extrair insights e informações úteis dos dados.**
D) Armazenar e gerenciar grandes volumes de dados.
****E) Realizar consultas complexas em tempo real.

4 - Qual das seguintes opções é um exemplo de uma IDE utilizada para interagir com bancos de dados?

~~A) Jupyter Notebook.~~

B) Eclipse.

C) Visual Studio Code.

D) IntelliJ IDEA.

**E) DBeaver.**

5 - O que significa a sigla "IDE"?

A) Integrated Database Engine (Motor de Banco de Dados Integrado).

B) Interactive Data Exploration (Exploração Interativa de Dados).
C) Integrated Data Envinroment (Ambiente de Dados Integrado).

**D) Integrated Development Environment (Ambiente de Desenvolvimento Integrado).**
E) Intelligent Data Extraction (Extração Inteligente de Dados).

---