# Em Busca da Playlist Perfeita no Spotify

Proposta de criação da funcionalidade de um Sistema de Recomendação: a partir de um item específico (música) de um determinado catálogo (Spotify), criar uma lista automática (playlist) contendo N itens semelhantes àquele selecionado.

## Entendendo o Problema / Coleta dos Dados

📌 O Spotify é uma plataforma de conteúdo de áudio presente em 178 países e contém 70 milhões de músicas. 

Como a própria plataforma descreve, a indústria da música está mudando de uma relação baseada em compra e posse de áudio, para um modelo de streaming on demand, em que os usuários consomem qualquer conteúdo disponível, conforme sua vontade.

Contribui muito para a experiência do usuário que a ele seja recomendado conteúdo que, muitas vezes, ele não conheceria por conta própria, enquanto que, para a empresa, é importante ter seu catálogo amplamente reproduzido (e não somente uma pequena parte dele), a fim de gerar mais receita. Assim nasce a importância dos Sistemas de Recomendação.

📌 Esta aplicação será construída da seguinte forma: **o usuário escolhe uma música do catálogo e, com ajuda de um modelo de predição, gera-se uma playlist de músicas semelhantes, com base nos atributos sonoros das faixas, nas músicas relacionadas, e nas preferências dos demais usuários**. O modelo deverá contar com as seguintes características:

- gerar playlists com uma quantidade específica de itens (digamos, 30 músicas);
- capacidade de criar playlists não-estáticas, isto é, gerar diferentes listas dada uma mesma música, mesmo que existam alguns itens que repitam de uma playlist para outra
- gerar playlists diversificadas, priorizando que sejam apresentadas faixas semelhantes, mas que sejam de álbuns e artistas diferentes entre si, a fim de que o usuário tenha uma experiência mais abrangente do catálogo do Spotify

📌 Pretende-se coletar uma quantidade abrangente de dados do catálogo do Spotify (tanto de usuários, quanto de músicas) para que se possa construir um modelo capaz de aprender a relação entre as faixas, e as preferências entre os usuários. Será utilizada a linguagem Python, e algumas de suas bibliotecas mais populares, como Pandas (análise de dados), Seaborn (visualização), Scikit Learn (aprendizado de máquinas), dentre outras que se façam necessárias.

📌 Este projeto usará a API do Spotify como fonte dos dados!

### Acesso ao Projeto no GitHub

O projeto estará disponível no GitHub através do link abaixo (atualmente está disponível uma versão 'Rascunho' do que esta aplicação virá a ser): 

[GitHub - jpborgesmoura/songs_recommender_system: Projeto prático de Recomendação de músicas, usando dataset do Spotify](https://github.com/jpborgesmoura/songs_recommender_system)
