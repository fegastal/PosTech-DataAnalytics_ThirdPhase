# FASE 03 - AULA 06 - RECOMENDAÇÕES COM O ALGORITMO ALS

Anotações sobre a sexta aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337986&amp;sesskey=aUi3fmwArb](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337986&amp;sesskey=aUi3fmwArb)

Temas abordados:

- Algoritmos de recomendação ALS (**Alternating Least Squares**) são uma abordagem eficaz para sistemas de recomendação que utilizam técnicas de aprendizado de máquina.
- São amplamente empregados em plataformas online para oferecer sugestões personalizadas aos(às) usuários(as), com base em suas preferências e histórico de intenções.
- Opera por meio de um processo interativo que estima a matriz de preferências de usuários e a matriz de características dos itens, minimizando a soma dos quadrados dos erros entre as avaliações reais e as estimadas.
- Abordagem flexível e escalável torna o ALS uma escolha popular para recomendação de produtos, músicas, filmes e outros conteúdos, permitindo que as empresas aprimorem a experiência do usuário e aumentem a taxa de engajamento.

---

## Parte 1 | INTRODUÇÃO A SISTEMAS DE RECOMENDAÇÃO

São técnicas de software que fornecem sugestões de itens a serem recomendados para um(a) usuário(a).

As sugestões fornecidas nos sistemas de recomendação visam ajudar os(as) usuários(as) em vários processos de tomada de decisão, bem como quais itens comprar, quais músicas escutar ou quais notícias ler.

Provaram ser valiosos por ajudar as pessoas a lidarem com a sobrecarga de informações, ao filtragem e recomendarem o que seria de interesse a elas.

Para o comércio, tornou-se uma das ferramentas mais poderosas e populares ao recomendar produtos ou serviços de acordo com os hábitos dos(as) usuários(as).

Existem duas arquiteturas básicas no uso de recomendação de sistemas, que são:

**1 SISTEMAS DE RECOMENDAÇÃO BASEADO EM CONTEÚDO**

O foco é nas propriedades dos itens. Similaridade de um item recomendado será medida pela similaridade com as propriedades do item que o(a) usuário(a) tenha adquirido ou pesquisado anteriormente.

Exemplo de uso do modelo baseado em conteúdo ou item, temos:

_ Produtos recomendados com base em sua compra ou pesquisa (e-commerce).

_ Sons parecidos que começam a tocar após o término de sua playlist (Spotify).

**2 SISTEMAS DE RECOMENDAÇÃO COM FILTRAGEM COLABORATIVA**

Baseado em filtragem colaborativa, o foco é na relação entre usuários e itens.

A similaridade dos itens é determinada pela similaridade da avaliação deles, pelos(as) usuários(as) que tenham avaliado os mesmos itens, ou seja: se os(as) usuários(as) tiverem avaliado itens com notas similares, provavelmente eles(as) têm gostos parecidos e aceitam recomendações com base nesse critério.

_  Pessoas que você talvez conheça, recomendação de amigos (Facebook);

_ Recomendação de sons para escutar (Spotify).

---

## Parte 2 | ARQUIVOS DE APOIO

**1 CRIAÇÃO DO SISTEMA DE RECOMENDAÇÃO**

Dica: para simplificar a vida e não precisar de nenhuma instalação adicional na sua máquina, utilizar o Google Colab.

Comece iniciando a sessão Spark: após a preparação do ambiente e do Spark ter sido encontrado no sistema, cria-se a sessão Spark:

`spark = SparkSession.builder.master(’local[*]’).getOrCreate()`

Carregar os dados: o conjunto de dados escolhido pertence ao Movielens. Estamos usando ele em formato txt e os dados, em cada linha, correspondem ao id do usuário, id do filme, nota e timestamp, conforme é possível ver na figura 2 “Amostra do conjunto de dados original”:

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled.png)

No código da fig 03, instanciamos os dados na variável lines com o **RDD (Resilient Distributed Dataset)**, a principal estrutura de dados do Spark. Ela permite trabalhar com computação distribuída, ou seja: os dados estão distribuídos entre os nós do cluster e controlados pelo nó master.

Dessa forma, é possível processá-los em paralelo, aumentando a **velocidade** de processamento.

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%201.png)

Agora, precisamos separar as entradas que vieram juntas. 

1 | É necessário separar os valores a cada “::” encontrado, com o objetivo de obter um array com 4 itens. Desse modo, usa-se o **método split**, responsável por isso. 

2 | Também usaremos a **função map**, que mapeia a operação, que está entre parênteses, para todas as linhas do RDD.

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%202.png)

3 | Transformar em Row → com o **módulo Row**, o RDD faz transformação para linhas do tipo Row. Ela é necessária porque também serão mapeados nomes e posições das colunas, instanciando tudo na variável ratingsRDD.

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%203.png)

4 | Apresentar dados em tabela → o próximo passo é dispor as informações em **formato de tabela**.

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%204.png)

5 | Obteremos a visualização da figura 7 → “DataFrame exibido com **ratings.show**()”

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%205.png)

6 | O modelo: nessa etapa, divide-se o conjunto de dados em porções para training e test. Em seguida, instancia-se o modelo ALS, indicando os parâmetros de quantidade máxima de iterações, coeficiente de aprendizado, colunas utilizadas e desconsiderando o usuário que tiver coldstart, caso ocorra.

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%206.png)

7 | Treinamento de teste: a seguir, treinamos o modelo com o DataSet de treinamento utilizando o als.fit() e aplicamos o modelo no conjunto de teste para fazer as predições com model.transform() e avaliação do modelo.

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%207.png)

8 | Recomendações: considerando todos os usuários do conjunto de dados, geramos **10 recomendações**.

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%208.png)

9 | Opcionalmente, foi feita a **transposta da matriz de ratings** a fim de recomendar usuários em potencial para itens específicos.

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%209.png)

10 | Podemos visualizar, também, filmes recomendados por usuários:

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%2010.png)

![Untitled](FASE%2003%20-%20AULA%2006%20-%20RECOMENDAC%CC%A7O%CC%83ES%20COM%20O%20ALGORITM%20b3d7a0b0ae9545a7a5317362ad8d2e90/Untitled%2011.png)

11 | Além dessa demonstração, são inúmeras as análises que podem ser realizadas com o DataSet em questão, conforme o objetivo de exploração e utilidade a que se destina.

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Quais são as principais vantagens do algoritmo ALS em sistemas de recomendação?

~~A) Leva em consideração as preferências dos usuários.~~

B) Pode lidar com dados esparsos. (?)

C) Nenhuma das opções anteriores. (?)
~~D) É computacionalmente eficiente para grandes conjuntos de dados.~~

E) Pode lidar com atributos complexos dos itens. (?)

2 - Qual é uma desvantagem do algoritmo ALS em sistemas de recomendação?

~~A) Pode levar a recomendações tendenciosas e polarizadas.~~
****B) Requer muitos recursos computacionais, tornando-o lento para grandes conjuntos de dados. (?)
****~~C) Nenhuma das opções anteriores.~~
****D) Não é capaz de lidar com dados esparsos. (?)
~~E) Geralmente fornece recomendações irrelevantes para os usuários.~~

3 - O algoritmo ALS é um método de filtragem colaborativa ou baseado em conteúdo?

A) Baseado em conteúdo.
B) Nenhuma das opções anteriores.
****C) Não se enquadra em nenhuma dessas categorias.
**D) Filtragem colaborativa.**
E) É uma combinação de filtragem colaborativa e baseada em conteúdo.

4 - Qual é o objetivo principal do algoritmo ALS em sistemas de recomendação?

A) Agrupar usuários com preferências semelhantes.

B) Nenhuma das opções anteriores.
C) Recomendar itens populares aos usuários.
****D) Encontrar itens semelhantes com base em atributos comuns.
**E) Prever a classificação de um item por um usuário.**

5 - O algoritmo ALS requer informações sobre os atributos dos itens?

A) O algoritmo ALS só funciona corretamente quando há poucos atributos dos itens.

**B) Não, o algoritmo ALS não leva em consideração os atributos dos itens.**
C) Nenhuma das opções anteriores.

D) Sim, é necessário fornecer atributos dos itens para que o ALS funcione corretamente.
**E) O algoritmo ALS pode funcionar tanto com ou sem atributos dos itens.**

---