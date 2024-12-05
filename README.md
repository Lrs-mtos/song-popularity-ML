# Song popularity ML model
This repository contains a ML project about predicting song popularity on Spotify.


# Guia para Abordagem e Análise de Problemas de Dados

## **Etapa 1: Abordar o Problema e Analisar o Panorama Geral**

### Definição do Problema:
1. **Defina o objetivo em termos de negócios**:
   - O objetivo do projeto é prever a tendência de uma música se tornar popular no Spotify, ajudando produtores e artistas a tomarem decisões ponderadas sobre lançamentos e campanhas de marketing. O sucesso será medido pela precisão das previsões e pelo impacto na identificação de músicas com alto potencial de popularidade.

2. **Como sua solução será usada?**:
   - A solução será usada por produtores musicais, artistas e equipes de marketing para identificar músicas com potencial de popularidade antes do lançamento. O modelo poderá ser integrado a uma plataforma de análise de dados onde os usuários inserem características das músicas (como nome da música, duração, artista etc), e o sistema fornece uma previsão (em porcentagem) sobre a probabilidade de sucesso. Isso permitirá decisões mais informadas e assertivas em campanhas de lançamento e divulgação.

3. **Quais são as soluções/alternativas atuais (caso existam)?**:
   - As soluções atuais incluem análises manuais de tendências por especialistas da indústria musical e ferramentas de análise de dados fornecidas pelo próprio Spotify, como o Spotify for Artists, que oferece informações sobre o desempenho das músicas após o lançamento. No entanto, essas soluções têm limitações:
      - As análises manuais dependem de experiência pessoal dos analistas e podem ser subjetivas.
      - As ferramentas do Spotify fornecem insights baseados em dados históricos, mas não oferecem previsões antes do lançamento de uma música.
   - Essas ferramentas atuais diferem do objetivo principal do nosso modelo, que busca superar essas limitações ao prever, de forma automatizada, a tendência de sucesso de uma música com base em suas características antes do lançamento, e não após.

4. **Como você deve abordar este problema?**:
   - A abordagem adotada será a de aprendizado supervisionado, uma vez que contamos com dados rotulados, ou seja, informações sobre músicas que já se tornaram populares (ou não) no Spotify. O objetivo é treinar o modelo para prever o potencial de sucesso de uma nova música com base nessas características. A partir desses exemplos rotulados, o modelo aprenderá a identificar padrões e fazer previsões.
   - Utilizaremos uma abordagem de processamento offline, pois o modelo de aprendizado supervisionado será treinado com dados históricos sobre músicas e sua popularidade, sem a necessidade de atualizações em tempo real.
  

   (OBS: Será online ou offline?)

5. **Como o desempenho deve ser medido?**:
   - Estabeleça métricas claras (ex.: precisão, recall, RMSE, etc.).

6. **A medida de desempenho está alinhada com o objetivo do negócio?**:
   - Valide se as métricas de sucesso técnico são compatíveis com o impacto esperado no negócio.

7. **Qual seria o desempenho mínimo necessário para alcançar o objetivo do negócio?**:
   - Estime o nível de desempenho técnico essencial para justificar o investimento.

8. **O que são problemas comparáveis?**:
   - Busque exemplos semelhantes já resolvidos e ferramentas reutilizáveis.

9. **Tem expertise humana disponível?**:
   - Identifique se há especialistas internos ou externos que podem ajudar.

10. **Como você resolveria o problema manualmente?**:
    - Pense em como o problema seria abordado sem automação para entender melhor a lógica por trás.

11. **Enumere as suposições que você (ou outras pessoas) fizeram até agora**:
    - Liste todas as hipóteses assumidas sobre os dados ou o problema.

12. **Verifique essas suposições, se possível**:
    - Teste e valide cada hipótese antes de seguir adiante.

---

## **Etapa 2: Obter os Dados**

1. **Liste os dados de que você precisa e de quanto precisa**:
   - Vamos utilizar todos os dados disponíveis no dataset, exceto track_id, track_album_id, playlist_name, playlist_id e playlist_subgenre. Esses dados não são relevantes para a previsão de popularidade da música, pois não influenciam diretamente as características musicais ou o desempenho da faixa em plataformas como o Spotify. As variáveis focadas serão aquelas que descrevem a música em termos de gênero, duração e outros atributos que impactam sua aceitação e sucesso.

2. **Encontre e documente onde você pode obter esses dados**:
   - Utilizaremos o dataset disponível no Kaggle, através do link: https://www.kaggle.com/datasets/joebeachcapital/30000-spotify-songs/data. Este conjunto de dados contém informações detalhadas sobre 30.000 músicas do Spotify, incluindo características relevantes para nossa análise. Ele será a fonte principal para treinar e testar o modelo de previsão de popularidade.

3. **Verifique quanto espaço esses dados ocuparão**:
   - De acordo com a descrição do dataset, ele possui um tamanho de 7,98 MB. Portanto, estimamos que esse é o espaço necessário para armazenar os dados completos, que incluem as informações detalhadas sobre as 30.000 músicas do Spotify.

4. **Verifique as obrigações legais e obtenha autorização, se necessário**:
   - Confirme o cumprimento de regulamentações de privacidade (ex.: LGPD, GDPR).

5. **Obtenha permissões de acesso**:
   - Garanta as autorizações adequadas para acessar os dados.

6. **Crie um workspace (com espaço de armazenamento suficiente)**:
   - Prepare o ambiente para análise (ex.: pastas, repositórios, etc.).

7. **Obtenha os dados**:
   - Realize o download, coleta ou integração de dados.

8. **Converta os dados em um formato que você possa manipular com facilidade (sem alterar os próprios dados)**:
   - Normalize ou transforme para CSV, JSON, SQL, entre outros.

9. **Assegure que as informações confidenciais sejam excluídas ou protegidas**:
   - Aplique anonimização ou outras práticas de segurança.

10. **Verifique o tamanho e o tipo de dados**:

    | **Variável**                   | **Descrição**                                            | **Tipo de Dado**           |
    |--------------------------------|----------------------------------------------------------|----------------------------|
    | **track_id**                   | ID único da música                                       | Categórico (nominal)       |
    | **track_name**                 | Nome da música                                           | Textual                    |
    | **track_artist**               | Nome do artista                                          | Categórico (nominal)       |
    | **track_popularity**           | Popularidade da música (0 a 100)                         | Numérico (contínuo)        |
    | **track_album_id**             | ID único do álbum                                        | Categórico (nominal)       |
    | **track_album_name**           | Nome do álbum                                            | Textual                    |
    | **track_album_release_date**   | Data de lançamento do álbum                              | Temporal                   |
    | **playlist_name**              | Nome da playlist                                         | Textual                    |
    | **playlist_id**                | ID da playlist                                           | Categórico (nominal)       |
    | **playlist_genre**             | Gênero da playlist                                       | Categórico (nominal)       |
    | **playlist_subgenre**          | Subgênero da playlist                                    | Categórico (nominal)       |
    | **danceability**               | Adequação da música para dançar (0.0 a 1.0)              | Numérico (contínuo)        |
    | **energy**                     | Energia da música (0.0 a 1.0)                            | Numérico (contínuo)        |
    | **key**                        | Tom principal da música (0 a 11; -1 para indeterminado)  | Categórico (ordinal)       |
    | **loudness**                   | Volume médio da música em decibéis                       | Numérico (contínuo)        |
    | **mode**                       | Modo da música (0 = menor, 1 = maior)                    | Categórico (binário)       |
    | **speechiness**                | Presença de palavras faladas (0.0 a 1.0)                 | Numérico (contínuo)        |
    | **acousticness**               | Confiança de ser acústica (0.0 a 1.0)                    | Numérico (contínuo)        |
    | **instrumentalness**           | Confiança de ser instrumental (0.0 a 1.0)                | Numérico (contínuo)        |
    | **liveness**                   | Probabilidade de ser gravada ao vivo (0.0 a 1.0)         | Numérico (contínuo)        |
    | **valence**                    | Positividade musical (0.0 a 1.0)                         | Numérico (contínuo)        |
    | **tempo**                      | Tempo médio em batidas por minuto (BPM)                  | Numérico (contínuo)        |
    | **duration_ms**                | Duração da música em milissegundos                       | Numérico (contínuo)        |

12. **Amostre um conjunto de teste, deixe-o de lado e nem coloque a mão nele**:
    - Separe os dados de teste para validação posterior, evitando data snooping.

