# Como criar um modelo de previsão no Azure

1. Acesse o Azure Portal com a sua conta e acesse a página ML Automatizado;
2. Crie um novo ML Automatizado seguindo os seguintes passos, clicando em Avançar sempre que preciso:
   ## Configurações Básicas
   * Nome do Trabalho: `mslearn-bike-automl`
   * Novo nome do experimento: `mslearn-bike-rental`
   * Descrição: `Automated machine learning for bike rental prediction`
   * Marcas: `None`
   ## Tipos de tarefa e dados
   * Selectionar tipo de tarefa: `Regression`
   * Selectionar os dados: Crie um novo com as seguintes configurações:
       ### Data type
       * Nome: `bike-rentals`
       * Descrição: `Historic bike rental data`
       * Tipo: `Tabular`
       ### Fonte de Dados
       * De arquivos da Web
       ### Data type
       * URL da Web: `https://aka.ms/bike-rentals`
       * Ignorar validação de dados: `OFF`
       ### Configurações
       * Formato do arquivo: `Delimited`
       * Delimitador: `Comma`
       * Codificação: `UTF-8`
       * Cabeçalhos de coluna: `Only first file has headers`
       * Ignorar linhas: `None`
       * Conjunto de dados com dados de várias linhas: `OFF`
       ### Esquema
       * Incluir todas as colunas menos a `Path`
   * Clique em **Criar**. Após ser criado, selecione `bike-rentals` e clique em avançar.
   ## Configurações de tarefas
   * Tipo de tarefa: `Regression`
   * Dados: `bike-rentals`
   * Coluna de destino: `Rentals (integer)`
   * Exibir definições de configuração adicionais
       * Métrica primária: `Normalized root mean squared error`
       * Explicar o melhor modelo: `OFF`
       * Usar todos os modelos suportados: `OFF`
       * Modelos permitidos: `RandomForest LightGBM`
   * Limites
       * Máximo de avaliações: `3`
       * Máximo de avaliações simultâneas: `3`
       * Máximo de nós: `3`
       * Limite de pontuação da métrica: `0.085`
       * Tempo limite do experimento: `15`
       * Tempo limite de iteração: `15`
       * Habilitar encerramento antecipado: `ON`
       * Tipo de validação: `Train-validation split` -> 10
       * Dados de teste: `None`
   ## Computação
   * Selecione o tipo de computação: `Serveless`
   * Tipo de máquina virtual: `CPU`
   * Tipo de máquina virtual: `Dedicado`
   * Tamanho da máquina virtual: `Standard_DS3_V2`
   * Número de instâncias: `1`
4. Submeta e espere a conclusão.

# Como testar o serviço

1. no Azure Machine Learning Studio, no menu à esquerda, selecione `Endpoints` e abra o endpoint `predict-rentals`;
2. Na página do endpoint, selecione a aba `Test`;
3. na opção `Inserir dados para teste de ponto de extremidade` insira:
```
 {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }
```
4. Clique em `Testar`;
5. Confira o resultado que inclui, o número previsto de aluguéis, baseado no que foi inserido. Similar a isso:
```
 {
   "Results": [
     444.27799000000000
   ]
 }
```
