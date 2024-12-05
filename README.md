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
   - Não, no grupo não existe ninguem que possua conhecimento suficiente referente a musica que possa
     ser considerado expertise, juntamente na área de ML. 

10. **Como você resolveria o problema manualmente?**:
    ### 1. Análise Exploratória de Dados
    O primeiro passo seria buscar possíveis correlações entre os dados para identificar padrões ou tendências. Isso ajudaria a entender como as variáveis se relacionam e     se há alguma indicação clara de influência na popularidade das músicas.

    ### 2. Uso de Métodos Estatísticos para Classificação
    Seria interessante utilizar métodos de classificação, seja por estatísticas ou outros métodos de aprendizado de máquina, para observar quais variáveis influenciam de     fato a popularidade das músicas. Essa análise ajudaria a identificar quais fatores são mais relevantes para a predição.
   
    ### 3. Consulta com Especialistas de Domínio
    Com as informações e padrões obtidos, é essencial consultar pessoas com domínio sobre aspectos como ritmo, energia e gênero musical. Esses especialistas podem            fornecer insights sobre como esses fatores podem influenciar positiva ou negativamente a compreensão e o sucesso de uma música.


11. **Enumere as suposições que você (ou outras pessoas) fizeram até agora**:
    ### 1. Variável `track_popularity` como Métrica de Sucesso
    A variável `track_popularity` é considerada uma boa métrica para determinar o sucesso de uma música, assumindo que ela reflete com precisão a popularidade e 
    aceitação de uma faixa pelo público. Nesse projeto, assume-se que essa métrica é o melhor indicador de sucesso, dado que mede diretamente a recepção e o alcance da 
    música.
   
   ### 2. Relevância das Variáveis Numéricas e Categóricas
   As variáveis numéricas e categóricas selecionadas são consideradas corretas e suficientes para a predição. Supõe-se que todos os atributos incluídos no modelo têm    
   relevância para prever a popularidade da música. A seleção de variáveis foi feita levando em conta a importância potencial de fatores como ritmo, energia e gênero, 
   que podem influenciar o sucesso da faixa.
   
   ### 3. Limpeza e Qualidade dos Dados
   Presume-se que os dados foram limpos adequadamente e que não contêm valores extremos que possam afetar de forma errada o modelo. A limpeza de dados é uma etapa 
   essencial para garantir que o modelo receba informações precisas e confiáveis, minimizando o risco de vieses ou distorções na análise.
   
   ### 4. Representatividade dos Dados
   A distribuição dos dados é assumida como representativa do que se encontra em um contexto real da indústria musical. Os dados coletados são considerados suficientes 
   para generalizar para o cenário da música popular, assumindo que eles cobrem uma variedade de gêneros, artistas e características de faixas típicas de sucessos na 
   indústria.

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
   
   O kaggle te disponibiliza o Dataset para download e possui uma versão em csv que ja é em formato válido para trabalhar
   com os dados,usando o seguinte código, obtemos o arquivo csv e realizamos um shape para visualizar o tamanho do Dataflame:
   ```python
      import numpy as np # linear algebra
      import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
      from sklearn.model_selection import train_test_split
      from sklearn.preprocessing import StandardScaler, OneHotEncoder
      from sklearn.compose import ColumnTransformer
      from sklearn.pipeline import Pipeline
   
      def returnDataFLame(file_path):
          try:
              df = pd.read_csv(file_path)
              return df
          except Exception as e:
              print(f"Erro ao ler o arquivo: {e}")
              return None
      
      # Ler o DataFrame
      df = returnDataFLame('/kaggle/input/30000-spotify-songs/spotify_songs.csv')
      
      # Verificar se o DataFrame foi lido com sucesso
      if df is None or df.empty:
          print("Erro: o arquivo não é CSV ou está vazio")
      else:
          print(df.shape)
   ```
   **Resultado da execução:**
   ```css
      (32833, 23)
   ```
   

10. **Assegure que as informações confidenciais sejam excluídas ou protegidas**:

    Levando em consideração a finalidade desse modelo, chegamos a conclusão de que nenhum desses dados deva ser considerado como
    uma informação confidencial, por outro lado como se trata de uma musica que não foi lançada, e conterá informações como: nome
    do album e nome da música não sei se isso seria relevante em termos de vazar dados, acho que seria um sim se tivessemos trabalhando
    diretamente com o audio da música.

12. **Verifique o tamanho e o tipo de dados**:

    | **Variável**                   | **Descrição**                                            | **Tipo de Dado**           |
    |--------------------------------|----------------------------------------------------------|----------------------------|
    | **track_name**                 | Nome da música                                           | Textual                    |
    | **track_artist**               | Nome do artista                                          | Categórico (nominal)       |
    | **track_popularity**           | Popularidade da música (0 a 100)                         | Numérico (contínuo)        |
    | **track_album_name**           | Nome do álbum                                            | Textual                    |
    | **track_album_release_date**   | Data de lançamento do álbum                              | Temporal                   |
    | **playlist_genre**             | Gênero da playlist                                       | Categórico (nominal)       |
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

13. **Amostre um conjunto de teste, deixe-o de lado e nem coloque a mão nele**:
    ```python
      # Separando as variáveis independentes e a dependente, queremos prever a popularidade
      # de uma música, logo nossa variável de predição é a track_popularity
      X = df.drop(columns=['track_popularity'])
      y = df['track_popularity']
      
      # Tratando valores nulos do nosso df, se tiver algum valor nulo, removemos a linha referente
      X = X.dropna()
      y = y[X.index]
      
      # Identificar variáveis numéricas e categóricas
      numeric_features = X.select_dtypes(include=['int64', 'float64']).columns
      categorical_features = X.select_dtypes(include=['object']).columns
      
      # Definindo transformações para variáveis numéricas e categóricas
      numeric_transformer = StandardScaler()
      categorical_transformer = OneHotEncoder(drop='first')
      
      # Criando um pré-processador usando ColumnTransformer
      preprocessor = ColumnTransformer(
          transformers=[
              ('num', numeric_transformer, numeric_features),
              ('cat', categorical_transformer, categorical_features)
          ]
      )
      
      # 70% para treino e 30% para teste
      X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
      print(f"Tamanho do conjunto de treino: {X_train.shape[0]}")
      print(f"Tamanho do conjunto de teste: {X_test.shape[0]}")

