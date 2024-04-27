<h1>
    <a href="https://www.dio.me/">
     <img align="center" width="64 px" src="https://hermes.dio.me/lab_projects/badges/f38a62b8-2880-4fd2-82ff-ba263ce97cdb.png">
    </a>
    <span>
      Reconhecimento Facial e transformação de imagens em Dados no Azure ML
    </span>
</h1>

### Criar um recurso de serviços de IA do Azure

**01.** Acessar o portal do [Azure](https://portal.azure.com), e entrar com a conta da Microsoft associada à assinatura do 
Azure.

**02.** Clicar no botão **＋Create a resource** e pesquisar os serviços de IA do Azure. Selecionar `create` em **Azure AI 
services**. 
    
- Seremos levados a uma página para criar um recurso de serviços de IA do Azure. 

Adicionar as seguintes configurações:

- **Assinatura**: Minha assinatura do Azure.
- **Grupo de recursos**: Selecionar ou criar um grupo de recursos com um nome exclusivo.
- **Região**: East US.
- **Nome**: Inserir um nome exclusivo.
- **Nível de preços**: Standard S0.
- **Ao marcar esta caixa, confirmo que li e compreendi todos os termos abaixo**: Selecionado.

**03.** Selecionar **Review + create**, depois **Create**, e aguardar a conclusão da implantação.

### Conectar o recurso de serviço de IA do Azure ao Vision Studio

**01.** Acessar o [Vision Studio](https://portal.vision.cognitive.azure.com/gallery/featured).

**02.** Entrar e certificar-se de utilizar o mesmo diretório onde criamos o recurso de serviços de IA do Azure.

**03.** Na página inicial do Vision Studio, selecionar **View all resources** no título **Getting started with Vision**.

**04.** Na página **Select a resource to work with**, passar o cursor do mouse sobre o recurso que foi criado e marcar a 
caixa à esquerda do nome do recurso, e selecionar **Select as default resource**.

>❕**Observação**: Se o recurso não estiver listado, pode ser necessário atualizar a página.

**05.** Fechar a página de configurações selecionando o “**x**” no canto superior direito da tela.

### Extraia texto de imagens no Vision Studio

**01.** Acessar o [Vision Studio](https://portal.vision.cognitive.azure.com/gallery/featured).

**02.** Na página **Getting started with Vision** selecionar **Optical character recognition** e, em seguida, selecionar o bloco
**Extract text from images**.

**03.** No subtítulo **Try It Out**, ler a respeito da política de uso de recursos e marcar a caixa.

**04.** Selecionar https://aka.ms/mslearn-ocr-images para baixar **ocr-images.zip**. Em seguida, abrir a pasta.

**05.** No portal, selecionar **Browse for a file**, navegar até a pasta onde baixamos o arquivo **ocr-images.zip**. Selecionar
**advert.jpg**, e selecionar **Open**.

**06.** Agora vamos revisar o que é retornado:

- Em **Detected attributes**, qualquer texto encontrado na imagem é organizado em uma estrutura hierárquica de regiões,
  linhas e palavras.

- Na imagem, a localização do texto é indicada por uma caixa delimitadora, conforme mostrado aqui:

![](outputs/advert-bounding-boxes.png)

### Gerar legendas para uma imagem

As legendas das imagens estão disponíveis por meio dos recursos **Legenda** e **Legendas densas**.

**01.** Acessar o [Vision Studio](https://portal.vision.cognitive.azure.com/gallery/featured).

**02.** Na página **Getting started with Vision** selecionar a guia **Image analysis** e, em seguida, selecionar o bloco
**Add captions to images**.

**03.** No subtítulo **Try It Out**, ler a respeito da política de uso de recursos e marcar a caixa.

**04.** Selecionar https://aka.ms/mslearn-images-for-análise para baixar **image-análise.zip**. Abrir a pasta baixada e
localizar o arquivo chamado **store-camera-1.jpg** que contém a seguinte imagem:

![](inputs/store-camera-1.png)

**05.** Carregar a imagem **store-camera-1.jpg** arrastando-a para a caixa **Drag and drop files here**, ou navegando até 
ela através do sistema de arquivos.

**06.** Observar o texto da legenda gerado, visível no painel **Detected attributes** à direita da imagem.

- A funcionalidade **Caption** fornece uma única frase em inglês legível que descreve o conteúdo da imagem.

**07.** Em seguida, utilizar a mesma imagem para realizar **Dense captioning**. Retornar à página inicial do **Vision Studio**
e, como anteriormente, selecionar a guia **Image analysis** e, em seguida, selecionar o bloco **Dense captioning**.

- O recurso **Dense Captions** difere do recurso **Caption** porque fornece diversas legendas legíveis para uma imagem, 
uma descrevendo o conteúdo da imagem, e outras cobrindo os objetos essenciais detectados na imagem. Cada objeto detectado 
inclui uma caixa delimitadora, que define as coordenadas dos pixels na imagem associada ao objeto.

**08.** Passar o mouse sobre uma das legendas na lista de atributos **Detected**, e observar o que acontece na imagem.

![](outputs/dense-captioning.png)

Mover o cursor do mouse sobre as outras legendas da lista e observar como a caixa delimitadora muda na imagem para destacar 
a parte da imagem usada para gerar a legenda.

### Limpar

Excluir todos os recursos que não forem mais necessários para evita acumular custos desnecessários.

**01.** Acessar o portal do [Azure](https://portal.azure.com), e selecionar o grupo de recursos que contém o recurso que foi criado para o exercício.

**02.** Selecionar o recurso, selecionar **Delete**, e depois **Yes** para confirmar. O recurso é então excluído.