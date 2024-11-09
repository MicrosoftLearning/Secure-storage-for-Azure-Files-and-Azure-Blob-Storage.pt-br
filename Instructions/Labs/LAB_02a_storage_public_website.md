---
lab:
  title: 'Exercício 02a: fornecer armazenamento para o site público'
  module: Guided Project - Azure Files and Azure Blobs
---
O site da empresa fornece imagens de produtos, vídeos, literatura de marketing e histórias de sucesso do cliente. Os clientes estão localizados em todo o mundo, e a demanda está se expandindo rapidamente. O conteúdo é crítico e exige tempos de carga de baixa latência. Será importante acompanhar as versões do documento e restaurar rapidamente os documentos se eles forem excluídos.

## Diagrama de arquitetura

![Diagrama com uma conta de armazenamento e um contêiner de blobs.](../Media/task-2.png)

## Tarefas de habilidades
- Criar uma conta de armazenamento com alta disponibilidade.
- Garantir que a conta de armazenamento tenha acesso público anônimo.
- Criar um contêiner de armazenamento de blobs para os documentos do site.
- Habilitar a exclusão temporária para que os arquivos possam ser facilmente restaurados.
- Habilitar o controle de versão de blob. 

## Instruções para o exercício

## Criar uma conta de armazenamento com alta disponibilidade.

1. Crie uma conta de armazenamento para dar suporte ao site público.

    - No portal, pesquise e selecione `Storage accounts`.  
    - Selecione **+ Criar**. 
    - Em **Grupo de recursos**, selecione **Novo**. Digite um **nome** para seu grupo de recursos e selecione **OK**. 
    - Defina o **Nome da conta de armazenamento** como `publicwebsite`. Confirme se o nome da conta de armazenamento é exclusivo adicionando um identificador.
    - Adote os padrões para as outras configurações. 
    - Selecione **Examinar** e, em seguida, **Criar**.
    - Aguarde até a conta de armazenamento ser implantada e selecione **Ir para o recurso**.
         
1. Esse armazenamento exige alta disponibilidade em caso de interrupção regional. Além disso, habilite o acesso de leitura à região secundária, Saiba mais sobre a [redundância da conta de armazenamento](https://learn.microsoft.com/azure/storage/common/storage-redundancy#geo-redundant-storage).

    - Na conta de armazenamento, na seção **Gerenciamento de dados**, selecione a folha **Redundância**. 
    - Verifique se a opção **Armazenamento com redundância geográfica com acesso de leitura** está selecionada.
    - Revise as informações de localização primária e secundária. 

1. As informações no sítio público devem estar acessíveis sem exigir que os clientes façam logon.
    - Na conta de armazenamento, na seção **Configurações**, selecione a folha **Configuração**.
    - Verifique se a configuração **Permitir acesso anônimo de blob** está **Habilitada**.
    - Não se esqueça de **Salvar** suas alterações. 
  
   
## Criar um contêiner de armazenamento de blobs com acesso de leitura anônimo

1. O site público tem várias imagens e documentos. Crie um contêiner de armazenamento de blobs para o conteúdo. Saiba mais sobre os [contêineres de armazenamento](https://learn.microsoft.com/azure/storage/blobs/storage-blobs-introduction#containers).
    - Na conta de armazenamento, na seção **Armazenamento de Dados**, selecione a folha **Contêineres**. 
    - Selecionar **+ Contêiner**. 
    - Verifique se o **Nome** do contêiner é `public`. 
    - Selecione **Criar**. 
    
1. Os clientes devem conseguir visualizar as imagens sem serem autenticados. Configure o acesso de leitura anônimo para os blobs de contêiner públicos.  Saiba mais sobre [como configurar o acesso público anônimo](https://learn.microsoft.com/azure/storage/blobs/anonymous-read-access-configure?tabs=portal).
    - Selecione seu contêiner **público**. 
    - Na folha **Visão geral**, selecione **Alterar nível de acesso**. 
    - Verifique se o **Nível de acesso público** é **Blob (acesso de leitura anônimo somente para blobs)**.
    - Selecione **OK**. 

## Pratique o upload de arquivos e teste de acesso.

1. Para testes, carregue um arquivo no contêiner **público**. O tipo de arquivo não importa. Uma imagem ou um arquivo de texto pequeno é uma boa opção.  
    - Verifique se você está visualizando seu contêiner. 
    - Escolha **Carregar**. 
    - **Navegue até arquivos** e selecione um arquivo. Procure um arquivo de sua escolha. 
    - Escolha **Carregar**.
    - Feche a janela de carregamento, **atualize** a página e verifique se o arquivo foi carregado. 

1. Determine a URL do arquivo carregado. Abra um navegador e teste a URL. 
    - Selecione o arquivo carregado.
    - Na guia **Visão geral**, copie a **URL**.
    - Cole a URL em uma nova guia do navegador.
    - Se você carregou um arquivo de imagem, ele será exibido no navegador. Outros tipos de arquivo serão baixados. 

## Configurar exclusão temporária

1. É importante que os documentos do site possam ser restaurados se forem excluídos. Configure a exclusão temporária de blob por 21 dias. Saiba mais sobre a [exclusão temporária de blobs](https://learn.microsoft.com/azure/storage/blobs/soft-delete-container-enable?tabs=azure-portal)
    - Acesse a folha **Visão geral** da **conta de armazenamento**.
    - Na página **Propriedades**, localize a seção **Serviço blob**.
    - Selecione a configuração **Exclusão temporária de blobs**.
    - Verifique se a opção **Habilitar exclusão temporária para blobs** está **marcada**.
    - Altere a configuração **Manter blobs excluídos por (em dias** é **21**.
    - Você também pode **Habilitar a exclusão temporária para contêineres**. 
    - Não se esqueça de **Salvar** as alterações. 

1. Se algo for excluído, você precisará praticar o uso da exclusão temporária para restaurar os arquivos.
    - Navegue até o contêiner em que você carregou um arquivo.
    - Selecione o arquivo que você carregou e selecione **Excluir**.
    - Selecione **OK** para confirmar a exclusão do arquivo.  
    - Na página **Visão geral** do contêiner, alterne o controle deslizante **Mostrar blobs excluídos**. Essa alternância está à direita da caixa de pesquisa. 
    - Selecione o arquivo excluído e use as reticências mais à direita para **Cancelar a exclusão** do arquivo. 
    - Atualize o contêiner e confirme se o arquivo foi restaurado.     

## Configurar o controle de versão de blobs
1. É importante acompanhar as diferentes versões de documentos de produtos do site. Saiba mais sobre o [controle de versão de blobs](https://learn.microsoft.com/azure/storage/blobs/versioning-enable?tabs=portal).
    - Acesse a folha **Visão geral** da **conta de armazenamento**.
    - Na seção **Propriedades**, localize a seção **Serviço Blob**.
    - Selecione a configuração **Controle de versão**.
    - Verifique se a caixa de seleção **Habilitar controle de versão para blobs** está marcada.
    - Observe suas opções para **manter todas as versões** ou **excluir versões depois**. 
    - Não se esqueça de **Salvar** as alterações. 

1. Como você tem tempo, experimente restaurar versões de blob anteriores.
   - **Carregue** outra versão do arquivo de contêiner. Isso substituirá o arquivo existente. 
   - Sua versão anterior do arquivo está listada na página **Mostrar blobs excluídos**. 
    
## Estender seu aprendizado com o Copilot

O Copilot pode ajudar você em sua jornada de aprendizado. O Copilot pode oferecer informações técnicas básicas, etapas de alto nível, prós e contras, ajuda para solução de problemas, casos de uso, exemplos de codificação e muito mais. Para acessar o Copilot, abra um navegador Edge e escolha Copilot (canto superior direito). Reserve alguns minutos para experimentar essas solicitações.
+ O que é o Armazenamento de Blobs do Azure e quando ele deve ser usado?
+ Compare os diferentes modelos de redundância de armazenamento do Azure, destacando seus principais recursos e casos de uso.
+ O que são as camadas de armazenamento do Azure e como essas camadas podem economizar dinheiro?

## Saiba mais com treinamento individual

+ [Explore o Armazenamento de Blobs do Azure](https://learn.microsoft.com/training/modules/explore-azure-blob-storage/). Neste módulo, você conhecerá os principais recursos e funcionalidades do Armazenamento de Blobs do Azure.

## Principais aspectos a serem lembrados

Parabéns por concluir o laboratório. Aqui estão as principais lições desse laboratório. 
+ O Armazenamento de Blobs do Azure é otimizado para armazenar grandes quantidades de dados não estruturados. Dados não estruturados são dados que não estão de acordo com uma definição ou um modelo de dados específico, como texto ou dados binários.
+ A exclusão reversível para blobs protege um blob individual, instantâneo ou versão de exclusões ou substituições acidentais, mantendo os dados excluídos no sistema por um período de tempo especificado. 
+ Controle de versão de blobs, versões anteriores de um blob. Quando o controle de versão de blobs estiver habilitado, você poderá restaurar uma versão anterior de um blob para recuperar os dados, caso eles tenham sido modificados ou excluídos por engano.
+ Quando um contêiner é configurado para acesso anônimo, todos os clientes podem ler dados nesse contêiner.
