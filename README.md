# Em Busca da Playlist Perfeita no Spotify

Proposta de criação da funcionalidade de um Sistema de Recomendação: a partir de um item específico (música) de um determinado catálogo (Spotify), criar uma lista automática (playlist) contendo N itens semelhantes àquele selecionado.

## Etapas I & II - Entendendo o Problema / Coleta dos Dados

O Spotify é uma plataforma de conteúdo de áudio presente em 178 países e contém 70 milhões de músicas. 

Como a própria plataforma descreve, a indústria da música está mudando de uma relação baseada em compra e posse de áudio, para um modelo de streaming on demand, em que os usuários consomem qualquer conteúdo disponível, conforme sua vontade.

Contribui muito para a experiência do usuário que a ele seja recomendado conteúdo que, muitas vezes, ele não conheceria por conta própria, enquanto que, para a empresa, é importante ter seu catálogo amplamente reproduzido (e não somente uma pequena parte dele), a fim de gerar mais receita. Assim nasce a importância dos Sistemas de Recomendação.

Este projeto será feito com base no seguinte dataset disponível no Kaggle, em formato CSV:

[Spotify Dataset 1922-2021, ~600k Tracks](https://www.kaggle.com/yamaerenay/spotify-dataset-19212020-160k-tracks)

🔴 ATENÇÃO: O dataset foi excluído do Kaggle pelo próprio Spotify!!

🏆 Com base no dataset disponibilizado, o objetivo deste projeto será **construir um modelo de predição que recebe uma música do catálogo como entrada, e gere uma playlist de músicas semelhantes, com base nos atributos sonoros dos itens, e nos artistas relacionados**. O modelo deverá contar com as seguintes características:

- gerar playlists com uma quantidade específica de itens (digamos, 30 músicas);
- capacidade de criar playlists não-estáticas, isto é, gerar diferentes listas dada uma mesma música, mesmo que existam alguns itens que repitam de uma playlist para outra
- gerar playlists diversificadas, priorizando que sejam apresentadas faixas semelhantes, mas que sejam de álbuns e artistas diferentes entre si, a fim de que o usuário tenha uma experiência mais abrangente do catálogo do Spotify

📌 Este dataset contém 600 mil músicas do catálogo do Spotify e 1 milhão de artistas, bem como uma relação de artistas entre si, disponível em arquivo JSON.

🎼 A lista de atributos está descrita na página do Kaggle, sendo:

- Para os **artistas** temos: dados de identificação, gêneros relacionados e popularidade
- Para as **faixas**, temos; seus atributos sonoros variando tipicamente de 0 a 1 (acusticidade, energia, instrumentabilidade, etc) e demais características (gênero, artistas, data de lançamento, nome, e etc)

📌 Por não conter dados de usuários no dataset utilizado, as recomendações não terão aspectos personalizados por usuário, mas sim, serão baseados em conteúdo. Assim, o modelo será do tipo Content-Based Filtering:

[Content-based Filtering | Recommendation Systems | Google Developers](https://developers.google.com/machine-learning/recommendation/content-based/basics)

### Acesso ao Projeto no GitHub

O projeto está disponível no GitHub através do link abaixo: 

[GitHub - jpborgesmoura/songs_recommender_system: Projeto prático de Recomendação de músicas, usando dataset do Spotify](https://github.com/jpborgesmoura/songs_recommender_system)

## Etapa III - Análise Exploratória dos Dados

🔖 **DICIONÁRIO DE DADOS**

[DataFrame Artists](https://www.notion.so/a167ab6010154280b4e86a8f8c8779fa)

[DataFrame Tracks](https://www.notion.so/3d024e20561a4788b09c8ab2d76ea15b)

[DataFrame Related Artists](https://www.notion.so/c5f09b2facdb4c93983d809bada9b1ee)

---

💡**CONCLUSÕES**

**DataFrame Artists**

✔️ ID

1.   Cada artista possui um id único

✔️ FOLLOWERS

1. Considerando os quartis no método *describe*, identificamos que 25% de todo o dataset possui até 10 seguidores
2. 75% dos artistas possuem até 451 seguidores
3. Os demais artistas (25%) constam com uma quantidade "desproporcional" aos demais, chegando a terem mais de 78 milhões, como é o caso de Ed Sheeran
4. Identificamos, então, que 187.927 são outliers considerando a quantidade de seus Seguidores, o que mostra que, de forma macro, os artistas têm padrões de quantidade de seguidores muito diferentes entre si
5. É possível perceber que, quanto maior o número de Seguidores, menor a quantidade de Artistas com tal atributo

✔️ GENRES

1. Temos 5365 gêneros musicais do dataset (exceto 'não especificado')
2. Muitos gêneros existentes são, na verdade, subdivisões de outros gêneros com base em regionalidades. Ex.: (ukrainian folk, ukrainian hip hop, ukrainian indie, ukrainian metal, ukrainian pop)
3. Existem 68 subgêneros apenas de musicas italianas, 59 suecas, 25 turcas, entre outros
4. Talvez seja válido criar uma relação entre gêneros, assim como já existe entre os artistas, para criar recomendações

✔️ NAME

- É importante que os artistas de nome duplicado não sejam excluídos do dataset, isso porque podem haver perdas ao gerar recomendações (exclusão de faixas do catálogo)
- Ao invés disso, vamos vincular os registros homônimos, através do DataFrame *related_artists*
- **IMPORTANTE: necessário criar um método que relacione os artistas de mesmo nome no DataFrame related_artists**

✔️ POPULARITY

1. Observa-se que a Popularidade é um item que varia de 0 a 100 no dataset
2. Como é de se esperar, quanto maior o número de Seguidores, maior a Popularidade do Artista
3. O artista com maior popularidade (Justin Bieber), porém, não é o artista com maior nº de Seguidores (mas está no 3º quartil em nº de Seguidores, tendo 44 milhões)
4. 75% de todos os artistas do dataset possuem uma Popularidade até 14, o que indica que o dataset é composto por artistas que, em sua maioria, possuem baixa Popularidade
5. 82.156 artistas são outliers, considerando a Popularidade

**DataFrame Tracks**

✔️ ID

1. Cada faixa possui um id único

✔️ NAME

1.   Excluímos 71 canções sem nome, de um artista que não existe no **df_artists**

2.   Ainda excluimos mais de 60.000 faixas que estavam repetidas, caso consideremos nome da faixa e id do artista

✔️ POPULARITY

1.   Vamos comparar a popularidade das faixas, com a popularidade dos seus respectivos cantores

2.   Pra isso, vamos unir os dois DataFrames, através do comando *merge()*

3.   Com o **merge 'left'**, existirão músicas sem artista (e, consequentemente, sem Gênero)

4.   Porém, no próprio **df_artists**, existem, também, artistas sem Gênero (not specified)

5.   Isso deve ser levado em consideração, caso tais itens sejam mantidos no DataFrame

6.  Existem artistas de alta popularidade com canções de baixa - e alta! - popularidades

7.  O contrário, porém, não é verdadeiro, pois, artistas de baixa popularidade só possuem canções de baixa popularidade

🔴 **IMPORTANTE!**

**A partir deste ponto, temos os DataFrames originais, bem como o *df_merged*, usado p/ fazer correlações**

**O *df_merged* será usado para construção do modelo**

**Para análise das features individualmente, continuaremos usando os DataFrame originais**

✔️ DURATION_MS

1. A média de duração das músicas do dataset é de 03min50s.
2. 75% das canções possuem até 04min23s.
3. A faixa de maior duração do dataset possui 01h33min41s, chama-se โครงสร้างแห่งสิ่งที่เรียกว่าชีวิต, que em Português significa "A estrutura daquilo que se chama de Vida", e, na verdade, trata-se de uma palestra

![the_biggest_song.PNG](Em%20Busca%20da%20Playlist%20Perfeita%20no%20Spotify%2060de97b835ff47268309d606575b5f59/the_biggest_song.png)

1. Levando isso em consideração, identificamos que no DataFrame Tracks, também estão relacionadas itens diferentes de música, em formato de faixas (palestras, álbuns inteiros, concertos etc)
2. Vamos excluir do DataFrame todos os itens que não consideramos músicas, pois levarão a erro no futuro modelo
3. Considerando o atributo de duração individualmente, vamos entender
como música todos os itens que possuem entre 01min30s de 20 minutos
4. Existem 1024 registros com duração superior a 20 minutos e 7182 com menos de 1 minuto.

✔️ EXPLICIT

1. O dataset possui mais de 100.000 músicas com conteúdo explícito
2. Os gêneros com mais músicas explícitas são rap, hip hop e seus subgêneros

✔️ ARTISTS

1. Observa-se, com ajuda da coluna artists, que ainda possuimos mais itens no DataFrame Tracks que não se tratam de músicas, mas sim, de audiolivros divididos em faixas
2. Chegamos a esta conclusão ao pesquisar, no próprio Spotify, pelos artistas com maior quantidade de faixas
3. É provável que hajam, porém, mais faixas de audiolivros além daqueles cujos artistas são os de maior quantidade de faixas no DataFrame
4. **IMPORTANTE: deve-se criar uma estratégia para limpar estes itens do dataset, para evitar que o modelo os leve em consideração**

✔️ ID_ARTIST

✔️ RELEASE_DATE

1. A quantidade de faixas disponíveis no dataset aumentam proporcionalmente conforme a passagem dos anos (as últimas décadas possuem mais registros do que das décadas antigas)
2. Referente à evolução dos gêneros musicais:

> Nas décadas de 20 e 30 eram mais comuns as músicas de tango;

> Entre os anos 40 e 50, as músicas mais clássicas e o jazz estavam em voga;

> O rock começou a tomar protagonismo nos anos 60, e dominou até os anos 80, começando a dar espaço para outros gêneros a partir dos anos 90

> Nos anos 90, a música latina começou a ganhar espaço, e vem em destaque até os dias atuais

> A partir dos anos 2000, o dance pop começou a ganhar mais espaço, e até hoje ocupa espaço no pódio da maior quantidade de faixas

✔️ DANCEABILITY

✔️ ENERGY

✔️ KEY

✔️ LOUDNESS

✔️ MODE

✔️ SPEECHINESS

✔️ INSTRUMENTALNESS

✔️ LIVENESS

✔️ VALENESS

✔️ TEMPO

✔️ TIME_SIGNATURE
