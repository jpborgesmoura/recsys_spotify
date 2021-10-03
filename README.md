# Em Busca da Playlist Perfeita no Spotify

Proposta de criação da funcionalidade de um Sistema de Recomendação: a partir de um item específico (música) de um determinado catálogo (Spotify), criar uma lista automática (playlist) contendo N itens semelhantes àquele selecionado.

## Entendendo o Problema / Coleta dos Dados

O Spotify é uma plataforma de conteúdo de áudio presente em 178 países e contém 70 milhões de músicas. 

Como a própria plataforma descreve, a indústria da música está mudando de uma relação baseada em compra e posse de áudio, para um modelo de streaming on demand, em que os usuários consomem qualquer conteúdo disponível, conforme sua vontade.

Contribui muito para a experiência do usuário que a ele seja recomendado conteúdo que, muitas vezes, ele não conheceria por conta própria, enquanto que, para a empresa, é importante ter seu catálogo amplamente reproduzido (e não somente uma pequena parte dele), a fim de gerar mais receita. Assim nasce a importância dos Sistemas de Recomendação.

Este projeto será feito com base no seguinte dataset disponível no Kaggle, em formato CSV:

[https://www.kaggle.com/yamaerenay/spotify-dataset-19212020-160k-tracks](https://www.kaggle.com/yamaerenay/spotify-dataset-19212020-160k-tracks)

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

## Análise Exploratória dos Dados

🔖 **DICIONÁRIO DE DADOS**

[DataFrame Artists](https://www.notion.so/a167ab6010154280b4e86a8f8c8779fa)

[DataFrame Tracks](https://www.notion.so/3d024e20561a4788b09c8ab2d76ea15b)

[DataFrame Related Artists](https://www.notion.so/c5f09b2facdb4c93983d809bada9b1ee)

Link do Notion: https://www.notion.so/Em-Busca-da-Playlist-Perfeita-no-Spotify-d75bf318de1543a28dd05e74a2d0d6cf
