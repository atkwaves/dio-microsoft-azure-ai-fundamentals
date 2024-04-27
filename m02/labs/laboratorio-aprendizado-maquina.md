<h1>
    <a href="https://www.dio.me/">
     <img align="center" width="64px" src="https://hermes.dio.me/lab_projects/badges/87d332d0-5198-4a2f-b159-38c8c2976954.png">
    </a>
    <span>
      Trabalhando com Machine Learning na Prática no Azure ML
    </span>
</h1>

### Criar um workspace do Azure Machine Learning

**01.** Acessar o portal do [Azure](https://portal.azure.com), e entrar com a conta da Microsoft associada à assinatura do Azure.

**02.** Selecionar **+ Criar um recurso**, pesquisar `Machine Learning` e criar um recurso do **Azure Machine Learning**.

Adicionar as seguintes configurações:

- **Assinatura**: Assinatura do Azure.
- **Grupo de recursos**: Selecionar ou criar um grupo de recursos.
- **Nome**: Inserir um nome exclusivo.
- **Região**: Selecionar a região geográfica mais próxima. (Ex.:East US)
- **Conta de armazenamento**: Manter a conta de armazenamento padrão que será criada para o workspace.
- **Cofre de chaves**: Manter o cofre de chaves padrão que será criado para o workspace.
- **Insights de aplicativo**: Manter o recurso Application Insights padrão que será criado para o workspace.
- **Registro de contêiner**: Nenhum (Será criado um automaticamente quando implantarmos um modelo em um contêiner pela primeira vez).

**03.** Selecionar **Examinar + Criar**, e **Criar**. Aguardar até que o workspace seja criado (isso pode demorar alguns minutos), acessar o recurso implantado.

**04.** Selecionar **Iniciar o estúdio** (ou abrir uma nova guia do navegador, acessar o [Estúdio do Azure Machine Learning](https://ml.azure.com) e entrar usando a conta Microsoft). Fechar todas as mensagens exibidas.

**05.** No Estúdio do Azure Machine Learning, teremos o workspace recém-criado. Caso contrário, selecionar **Todos os workspaces** no menu à esquerda, e selecionar o workspace que acabamos de criar.

### Usar aprendizado de máquina automatizado para treinar um modelo

O aprendizado de máquina automatizado possibilita a exploração de uma variedade de algoritmos e parâmetros, permitindo o treinamento de diversos modelos para identificar o mais adequado aos nossos dados. Por exemplo, é possível utilizar um conjunto de dados contendo informações históricas sobre o aluguel de bicicletas para desenvolver um modelo capaz de prever a quantidade de aluguéis esperados em um determinado dia, levando em consideração fatores sazonais e meteorológicos.

>❕**Observação**: Os dados usados neste exercício são derivados do [Capital Bikeshare](https://www.capitalbikeshare.com/system-data) e são usados de acordo com o [contrato de licença](https://www.capitalbikeshare.com/data-license-agreement) de dados publicados.

**01.** No estúdio do [Azure Machine Learning](https://ml.azure.com/?azure-portal=true), ir para a página **ML Automatizado** (em **Criação**).

**02.** Criar um novo trabalho de ML automatizado com as seguintes configurações, utilizando **Avançar** conforme necessário para avançar dentro da interface do usuário:

**Configurações básicas**:

- **Nome do trabalho**: mslearn-bike-automl
- **Nome do novo experimento**: mslearn-bike-rental
- **Descrição**: Machine Learning automatizado para previsão de aluguel de bicicletas
- **Marcas**: Nenhuma

**Tipo de tarefa e dados**:

- **Selecionar tipo de tarefa**: Regressão
- **Selecionar conjunto de dados**: Criar um novo conjunto de dados com as seguintes configurações:
    - **Tipo de dados**:
        - **Nome**: bike-rentals
        - **Descrição**: Dados históricos de aluguel de bicicletas
        - **Tipo**: Tabular
    - **Fonte de dados**:
        - Selecionar **De arquivos da Web**
    - **URL da Web**:
        - **URL da Web**: https://aka.ms/bike-rentals
        - **Ignorar validação de dados**: Não selecionar
    - **Configurações**:
        - **Formato de arquivo**: Delimitado
        - **Delimitador**: Vírgula
        - **Codificação**: UTF-8
        - **Cabeçalhos de coluna**: Somente o primeiro arquivo tem cabeçalhos
        - **Ignorar linhas**: Nenhum
        - **O conjunto de dados contém dados multilinhas**: Não selecionar
    - **Esquema**:
        - Incluir todas as colunas que não sejam **Caminho**
        - Examinar os tipos detectados automaticamente

Selecionar **Criar**. Após a criação do conjunto de dados, selecionar o conjunto de dados de **aluguel de bicicletas** para continuar a enviar o trabalho do ML Automatizado.

**Configurações da tarefa**:

- **Tipo de tarefa**: Regressão
- **Conjunto de dados**: bike-rentals
- **Coluna de destino**: Aluguéis (inteiro)
- **Definições de configuração adicionais**:
    - **Métrica primária**: Erro quadrático médio da raiz normalizada
    - **Explicar o melhor modelo**: Não selecionado
    - **Usar todos os modelos com suporte**: Não selecionado. Vamos restringir o trabalho para experimentar apenas alguns algoritmos específicos.
    - **Modelos permitidos**: Selecionar apenas **RandomForest** e **LightGBM**. O ideal seria tentar usar o máximo possível, mas cada modelo adicionado aumenta o tempo necessário para executar o trabalho.
- **Limites**:
    - **Avaliações máximas**: 3
    - **Máximo de avaliações simultâneas**: 3
    - **Máximo de nós**: 3
    - **Limite de pontuação da métrica**: 0,085 (de modo que se um modelo atingir uma pontuação métrica da raiz do erro quadrático médio de 0,085 ou menos, o trabalho termina.)
    - **Tempo limite**: 15
    - **Tempo limite de iteração**: 15
    - **Habilitar encerramento antecipado**: Selecionado
- **Validação e teste**:
    - **Tipo de validação**: Divisão de validação de treinamento
    - **Percentual de dados de validação**: 10
    - **Conjunto de dados de teste**: Nenhum

**Computação**:

- **Selecionar tipo de computação**: Sem servidor
- **Tipo de máquina virtual**: CPU
- **Camada da máquina virtual**: Dedicada
- **Tamanho da máquina virtual**: Standard_DS3_V2*
- **Número de instâncias**: 1

>❕**Observação**: Se a assinatura restringir os tamanhos de VM disponíveis, escolha qualquer tamanho disponível.

**03.** Enviar o trabalho de treinamento. Ele é iniciado automaticamente.

**04.** Aguardar a conclusão do trabalho.

### Examinar o melhor modelo

**01.** Na guia **Visão geral** do trabalho de Machine Learning automatizado, podemos observar o resumo do melhor modelo.

>❕**Observação**: Podemos visualizar uma mensagem sob o status “Aviso: Pontuação de saída especificada pelo usuário atingida…”. Essa é uma mensagem esperada.

**02.** Selecionar o texto em **Nome do algoritmo** do melhor modelo para exibir os respectivos detalhes.

**03.** Selecionar a guia **Métricas** e selecionar os gráficos **residuais** e **predicted_true** se eles ainda não estiverem selecionados.

Examinar os gráficos que mostram o desempenho do modelo. O gráfico de resíduos mostra os resíduos (as diferenças entre valores previstos e reais) como um histograma. O gráfico predicted_true compara os valores previstos com os valores verdadeiros.

### Implantar e testar o modelo

**01.** Na guia **Modelo** para obter o melhor modelo treinado pelo trabalho de Machine Learning automatizado, selecionar **Implantar** e usar a opção **serviço Web** para implantar o modelo com as seguintes configurações:

- **Nome**: predict-rentals
- **Descrição**: Prever aluguéis de bicicleta
- **Tipo de computação**: Instância de Contêiner do Azure
- **Habilitar autenticação**: Selecionado

**02.** Aguardar até o início da implantação – isso pode levar alguns segundos. O **Status de implantação** para o ponto de extremidade **predict-rentals** será indicado na parte principal da página como **Em execução**.

**03.** Aguardar até que o **Status de implantação** mude para **Bem-sucedida**. Isso pode levar de 5 a 10 minutos.

### Testar o serviço implantado

**01.** Em Estúdio do Azure Machine Learning, no menu à esquerda, selecionar **Pontos de Extremidade** e abrir o ponto de extremidade em tempo real **predict-rentals**.

**02.** Na página do ponto de extremidade em tempo real de **previsão de aluguel**, exibir a guia **Teste**.

**03.** No painel **Dados de entrada para testar o ponto de extremidade**, substituir o modelo JSON pelos seguintes dados de entrada:

``` JSON
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

**04.** Clicar no botão **Testar**.

**05.** Revisar os resultados do teste, que incluem um número previsto de aluguéis com base nos recursos de entrada – semelhante ao seguinte:

```JSON
 {
   "Results": [
     444.27799000000000
   ]
 }
```

O painel de teste pegou os dados de entrada e usou o modelo que treinamos para retornar o número previsto de locações.

### Resumo Laboratório

Utilizamos um conjunto de dados históricos de locação de bicicletas para treinar um modelo. O modelo prevê o número de locações de bicicletas esperadas em um determinado dia, com base em recursos sazonais e meteorológicos.

### Limpar

O serviço Web que criamos está hospedado em uma Instância de Contêiner do Azure. Se não pretendemos utilizá-lo mais, devemos excluir o ponto de extremidade para evitar o acúmulo de uso desnecessário do Azure.

**01.** No estúdio do Azure Machine Learning, na guia **Pontos de extremidade**, selecionar o ponto de extremidade **predict-rentals**. Depois, selecionar **Excluir** e confirmar que desejamos excluir o ponto de extremidade.

