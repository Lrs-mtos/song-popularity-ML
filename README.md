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
   - Cenário 1 - Classificação:
      A medida utilizada será a sensibilidade/especificidade, sendo calculada como a proporção de exemplos realmente positivos dentre todos aqueles que o modelo classificou como positivos. Ou seja, se o modelo afirma que uma certa música vai ser popilar, a precisão irá medir a porcentagem de acertos dentre essas previsões.

   - Cenário 2 - Regressão:
      A medida utilizada será RMSE (Root Mean Squared Error) que é a raiz quadrada da média dos erros quadráticos. Ela mede a diferença entre os valores previstos pelo modelo e os valores reais, penalizando erros maiores de forma mais intensa do que erros pequenos.   

6. **A medida de desempenho está alinhada com o objetivo do negócio?**:
   - Cenário 1.0 - Classificação não arriscada:
      No caso em que o objetivo é classificar uma música como baixa, média, alta ou muito alta popularidade, a decisão sobre a métrica foca em não disperdiçar recursos com músicas sem potencial - como disse o cliente -, ou seja, os casos onde as falsas classificações de 'popular' (Falsos Positivos) são especialmente prejudiciais. Deve-se então ter a certeza de que, ao afirmar que a música será popular, estejamos o mais correto possível. A sensibiliddade é uma boa métrica nesse caso
   - Cenário 1.1 - Classificação arriscada:
      No caso em que o objetivo do cliente é arriscar em tendências, a métrica mais adequada seria a especificade.
   - Cenário 2 - Regressão:
      No caso em que o objetivo é prever a popularidade da música em uma escala numérica (de 0 a 100, como faz o dataset, por exemplo) não há classes discretas, mas sim um valor contínuo que indica um nível de popularidade. A métrica utilizada penaliza erros maiores de forma mais intensa - o cliente não quer perder dinheiro de nenhuma forma -. Além disso a vizualização dos dados fica mais clara - o cliente quer acompanhar os dados de perto - pois se trata de um modelo que traz o erro para a mesma unidade da variável alvo.

7. **Qual seria o desempenho mínimo necessário para alcançar o objetivo do negócio?**:
   - Cenário 1: O cliente declara que quer o mínimo de erros possível, disse que sua tolerância seria "de 10 músicas, quero que pelo menos 9 sejam certeiras". Com base nisso, a estimativa ficou de 90% de sensibilidade.
   - Cenário 2: O cliente declara que nesse caso deseja que a popularidade mínima que o faria investir seria um popularidade de 80 com pouca variação. Nesse caso, foi decidido que o RMSE poderia ser de no máximo 5 pontos. Utilizando o exemplo do cliente, o uso da música pode variar de 75 a 85, por exemplo.

8. **O que são problemas comparáveis?**:
   - Existem problemas comparáveis sim. Por exemplo, [alguns estúdios de cinema como a 20th Century Fox usam ML para verificar os interesses do público](https://turismomundo.com.br/como-os-estudios-de-cinema-usam-inteligencia-artificial-para-prever-os-interesses-dos-publicos-de-cinema/?utm_source=web-stories-generator).

9. **Tem expertise humana disponível?**:
   - Não, no grupo não existe ninguem que possua conhecimento suficiente referente a musica que possa
     ser considerado expertise, juntamente na área de ML. 

10. **Como você resolveria o problema manualmente?**:
    #### 1. Análise Exploratória de Dados
    O primeiro passo seria buscar possíveis correlações entre os dados para identificar padrões ou tendências. Isso ajudaria a entender como as variáveis se relacionam e     se há alguma indicação clara de influência na popularidade das músicas.

    #### 2. Uso de Métodos Estatísticos para Classificação
    Seria interessante utilizar métodos de classificação, seja por estatísticas ou outros métodos de aprendizado de máquina, para observar quais variáveis influenciam de     fato a popularidade das músicas. Essa análise ajudaria a identificar quais fatores são mais relevantes para a predição.
   
    #### 3. Consulta com Especialistas de Domínio
    Com as informações e padrões obtidos, é essencial consultar pessoas com domínio sobre aspectos como ritmo, energia e gênero musical. Esses especialistas podem            fornecer insights sobre como esses fatores podem influenciar positiva ou negativamente a compreensão e o sucesso de uma música.

    #### 4. Levantamento e validação de hipoteses
    De acordo com todas as informações reunidas acerca dos dados e do que foi discutido com especialistas, levantaria algumas hipoteses e buscaria uma forma de 
    validalas.  

12. **Enumere as suposições que você (ou outras pessoas) fizeram até agora**:
    #### 1. Variável `track_popularity` como Métrica de Sucesso
    A variável `track_popularity` é considerada uma boa métrica para determinar o sucesso de uma música, assumindo que ela reflete com precisão a popularidade e 
    aceitação de uma faixa pelo público. Nesse projeto, assume-se que essa métrica é o melhor indicador de sucesso, dado que mede diretamente a recepção e o alcance da 
    música.
   
    #### 2. Relevância das Variáveis Numéricas e Categóricas
    As variáveis numéricas e categóricas selecionadas são consideradas corretas e suficientes para a predição.
   
    #### 3. Limpeza e Qualidade dos Dados
    Presume-se que no dataflame os dados estão distribuidos de forma correta e não possuem nenhum tipo de valores extremos que possam atrapalhar na predição do modelo.
   
    #### 4. Representatividade dos Dados
    Os dados coletados são suficientes para generalizar para o cenário da música popular, assumindo que eles cobrem uma variedade de gêneros, artistas e 
    características de faixas típicas de sucessos na indústria.

13. **Verifique essas suposições, se possível**:
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
   
   No momento em que os dados são acessados, é possível encontrar um [link](https://opendatacommons.org/licenses/dbcl/1-0/) chamado "License". Nele é possível encontrar um documento detalhado sobre os direitos que você tem sobre o conteúdo do banco de dados, como usar, modificar, distribuir, sublicenciar e vender o conteúdo, e os termos sob os quais você pode usá-lo, incluindo o cumprimento da ODbL e a isenção de responsabilidade do Licenciante.

Em termos simples:

>Você tem ampla liberdade para usar o conteúdo, inclusive para fins comerciais.
>O Licenciante não garante que os dados estão corretos ou sem erros, e não será responsável por quaisquer danos resultantes do uso dos dados.
>O Licenciante não reivindica direitos autorais sobre dados factuais (como números ou observações).
>Portanto, se você estiver usando este conteúdo, deve estar ciente de que pode usar livremente os dados, mas também deve respeitar as condições da ODbL e entender que o Licenciante não se responsabiliza por eventuais problemas.


5. **Obtenha permissões de acesso**:

   De acordo com os dados da licença, não é necessário nenhum tipo de permissão de acesso específica.

6. **Crie um workspace (com espaço de armazenamento suficiente)**:
   - Foi preparado o ambiente para análise.

7. **Obtenha os dados**:
   - Foi realizado o download dos dados na [plataforma Kaggle](https://www.kaggle.com/datasets/joebeachcapital/30000-spotify-songs?resource=download).

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
   
      def returnDataFrame(file_path):
          try:
              df = pd.read_csv(file_path)
              return df
          except Exception as e:
              print(f"Erro ao ler o arquivo: {e}")
              return None
      
      # Ler o DataFrame
      df = returnDataFrame('/kaggle/input/30000-spotify-songs/spotify_songs.csv')
      
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

