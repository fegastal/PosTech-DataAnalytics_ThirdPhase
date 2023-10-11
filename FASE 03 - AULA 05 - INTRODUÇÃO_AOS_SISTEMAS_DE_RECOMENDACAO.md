# FASE 03 - AULA 05 - INTRODUÇÃO AOS SISTEMAS DE RECOMENDAÇÃO

Anotações sobre a quinta aula da terceira fase da PosTech FIAP **✨✨**

[https://on.fiap.com.br/mod/conteudoshtml/view.php?id=307799&c=8729&sesskey=mp0PcE8JII](https://on.fiap.com.br/mod/conteudoshtml/view.php?id=337985&amp;sesskey=Wfd1uQJe6L)

Temas abordados:

- Compreensão dos sistemas de recomendação e seu impacto nas experiências online.
- Analisar dados de usuários, identificar padrões e sugerir itens relevantes e personalizados.
- Filtragem colaborativa, recomendações baseadas em conteúdo e sistemas híbridos.

---

## Parte 1 | O QUE SÃO ALGORITMOS DE RECOMENDAÇÃO?

Algoritmos destinados a sugerir itens relevantes para os usuários. São realmente críticos em alguns setores, pois podem gerar uma grande quantidade de receita quando são eficientes ou ser uma maneira de se destacar significativamente dos concorrentes.

Há alguns anos, a Netflix organizou um desafio (o prêmio Netflix) onde o objetivo era produzir um sistema de recomendação com desempenho superior ao seu próprio algoritmo com um prêmio de 1 milhão de dólares para vencer.

Pontos importantes para construir seu próprio sistema de recomendação:

1 | Se você tiver um grande banco de dados e fizer recomendações online a partir dele, a melhor maneira seria dividir esse problema em 2 subproblemas: **1 (escolher os principais N candidatos) e 2 (classificá-los)**.

2 | Como você mede a qualidade do seu modelo? Em conjunto com as métricas de qualidade padrão, existem algumas métricas que são usadas especialmente para problemas de recomendação. São elas: **Recall e Precision**, **Average Recall** e **Average Precision**.

3 | Se estiver resolvendo problemas de recomendação com algoritmos de classificação, você deve pensar em gerar amostras negativas. Se um usuário comprou um item recomendado, você não deve acioná-lo como amostra positivva e outros como amostras negativas.

4 | Pense na pontuação online e na pontuação offline da qualidade do seu algoritmo. Um modelo de treinamento apenas em dados históricos pode levar a recomendações primitivas porque o algoritmo não saberá sobre novas tendências e preferências.

---

## Parte 2 | TIPOS DE ALGORITMOS DE RECOMENDAÇÃO

Os três principais são:

**1 | Filtragem colaborativa**

Usuários com experiências semelhantes em itens também têm probabilidades semelhantes de gostar de outros itens. Utiliza dados históricos de interações entre usuários e itens (como avaliações, compras, cliques) para identificar padrões de similaridade entre eles. Com base nessas similaridades, o sistema recomenda itens que outros usuários com gostos similares apreciaram.

Duas formas: 

- Abordagem baseada em usuário → recomenda itens com base nos interesses de usuários semelhantes
- Abordagem baseada em item → recomenda itens com base em características semelhantes aos itens previamente apreciados pelo usuário.

**2 | Filtragem baseada em conteúdo**

Utiliza características e atributos dos itens para fazer recomendações. Analisa informações descritivas sobre os itens e as combina com o perfil de preferências do usuário. Exemplo: sistema de recomendações de filmes → algoritmo pode considerar gênero, diretor, elenco e sinopse para sugerir filmes que possam agradar ao usuário com base em filmes que ele já assistiu e gostou.

Tende a ser mais personalizada, pois se concentra nas preferências específicas do usuário em vez de depender exclusivamente das opiniões de outros usuários.

**3 | Sistemas Híbridos**

Combinam abordagens de filtragem colaborativa e filtragem baseada em conteúdo para melhorar a qualidade das recomendações. A ideia é que, ao combinar as duas técnicas, seja possível migrar as limitações de cada uma individualmente.

Algoritmos hibridos podem ser desenvolvidos de várias maneiras, como: 

- Utilizando filtragem colaborativa para inicialmente fazer recomendações amplas com base em tendências populares;
- Em seguida, refinando essas sugestões com a filtragem baseada em conteúdo para personalizá-las de acordo com as preferências do usuário.

Outra abordagem comum é atribuir pesos diferentes às duas técnicas, dependendo do contexto da recomendação.

Esses três tipos de algoritmos de recomendação desempenham um papel essencial em diversas aplicações, desde sistemas de entretenimento até plataformas de e-commerce, tornando-se uma parte fundamental da experiência do usuário em muitos serviços digitais.

---

## Parte 3 | CASOS DE USO REAL DE SISTEMAS DE RECOMENDAÇÃO

**1 | Filtragem colaborativa → Netflix**

O serviço de streaming de vídeo Netflix utiliza a filtragem colaborativa para fazer recomendações personalizadas de filmes e séries para seus usuários.

Com base nas avaliações e no histórico de visualização de cada usuário, o algoritmo identifica padrões de comportamento semelhantes entre diferentes usuários.

Exemplo: se um usuário A e um usuário B têm avaliações semelhantes para um conjunto de filmes, o sistema pode inferir que eles têm gostos muito similares. Em seguida, o algoritmo pode recomendar filmes que o usuário A assistiu e gostou a outros usuários que demonstraram preferências semelhantes, como o usuário B.

**2 | Filtragem baseada em conteúdo → Spotify**

O serviço de streaming de música Spotify utiliza a filtragem baseada em conteúdo para fazer recomendações de músicas e playlists personalizadas para seus usuários. 

O algoritmo analisa os atributos musicais das faixas que o usuário já ouviu e apreciou, como gênero, artista, ritmo e letra. Com base nesses atributos, o sistema pode sugerir novas músicas e playlists que se alinhem com o gosto musical específico do usuário. 

Por exemplo, se um usuário ouviu muitas músicas de artistas pop e playlists com "vibração de festa", o sistema pode recomendar outras músicas pop animadas que se adequem ao seu perfil musical.

**3 | Sistemas híbridos → Amazon**

A plataforma de e-commerce Amazon utiliza um sistema híbrido para fazer recomendações de produtos para seus usuários. 

O algoritmo combina a filtragem colaborativa, que leva em conta o histórico de compras e interações dos usuários, com a filtragem baseada em conteúdo, que analisa as características dos produtos. 

Por exemplo, se um usuário comprou um smartphone com especificações técnicas específicas (filtragem baseada em conteúdo), o sistema pode recomendar acessórios ou produtos relacionados que outros usuários que compraram smartphones semelhantes também adquiriram (filtragem colaborativa).

---

### **FAST TEST - TREINE SUA PROFICIÊNCIA**

1 - Qual é a definição correta de um sistema de recomendação?

A) Um sistema que recomenda produtos aleatórios aos usuários.

B) Um sistema que coleta informações pessoais dos usuários sem seu consentimento.

C) Um sistema que fornece atualizações de notícias em tempo real.
**D) Um sistema que analisa o comportamento e as preferências dos usuários para fazer recomendações personalizadas.**

E) Um sistema que exibe anúncios publicitários aos usuários.

2 - Qual é a importância da filtragem colaborativa em sistemas de recomendação?

A) Melhorar a velocidade de carregamento das páginas do site.
**B) Fornecer recomendações com base nas preferências dos amigos ou usuários semelhantes.**
C) Identificar a localização geográfica dos usuários.
****D) Identificar a localização geográfica dos usuários.
E) Enviar notificações por email aos usuários.

3 - O que é a serendipidade em sistemas de recomendação?

A) A medida que indica a quantidade de itens diferentes recomendados aos usuários.
**B) A medida que indica a capacidade do sistema de fazer recomendações surpreendentes e úteis.**
C) A medida que indica o quão aleatórias são as recomendações feitas.
D) A medida que indica o número de recomendações feitas por dia.
E) A medida que indica o quão precisas são as recomendações feitas.

4 - O que é a avaliação de precisão em sistemas de recomendação?

A) A medida que indica quantos usuários estão satisfeitos com as recomendações recebidas.

**B) A medida que indica a relevância das recomendações feitas em relação às preferências do usuário.**
C) A medida que indica quantas recomendações são exibidas aos usuários.
****D) A medida que indica a quantidade de itens disponíveis para recomendação.
E) A medida que indica o quão rápida é a resposta do sistema de recomendação.

5 - O que é a abordagem baseada em conteúdo em sistemas de recomendação?

A) Uma técnica que exibe anúncios personalizados com base nas preferências do usuário.

B) Uma técnica que permite que os usuários filtrem as recomendações com base em seu próprio critério.
C) Uma técnica que permite que os usuários classifiquem os itens em ordem de preferência.

**D) Uma técnica que analisa as características dos itens e recomenda itens semelhantes aos que o usuário gostou anteriormente.**
E) Uma técnica que recomenda apenas produtos populares.