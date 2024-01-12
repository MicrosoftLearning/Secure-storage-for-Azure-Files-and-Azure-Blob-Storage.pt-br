---
demo:
  title: 'Demonstração 02: criar e configurar o armazenamento de blobs'
  module: Guided Project - Azure Files and Azure Blobs
---


## Demonstração – Criar e configurar o armazenamento de blobs.

Nesta demonstração, explore o armazenamento de blobs.

## Revisar configurações de armazenamento de blobs

1. [Slide de apoio] Antes de iniciar a demonstração, revise os usos e a organização do armazenamento de blobs. Quais de nossos grupos empresariais precisarão de armazenamento de blobs?

1. Acesse o **portal do Azure**.

1. Você pode continuar usando a conta de armazenamento anterior. 

1. Selecione a guia **Visão geral**.

1. [Slide de apoio] Na seção **Serviço Blob**, realce a configuração **Camada de acesso padrão**. Explique como o conteúdo corporativo pode estar na camada de acesso frequente. As informações de auditoria podem estar na camada de acesso esporádico. Logs ou literatura de marketing sazonal podem estar na camada de arquivos. Saiba mais, [Níveis de acesso para armazenamento de blobs](https://docs.microsoft.com/azure/storage/blobs/access-tiers-overview).

1. [Slide de apoio] Na seção **Serviço Blob**, realce as configurações de **exclusão temporária**. Isso seria importante para o site público no caso de algo ser acidentalmente excluído ou substituído. Os alunos praticarão a exclusão temporária no laboratório. Saiba mais, [Exclusão temporária de blobs](https://learn.microsoft.com/azure/storage/blobs/soft-delete-blob-overview).

1. Na seção **Serviço Blob**, aponte a configuração **Controle de versão**. Isso pode ser importante para o departamento de Marketing. A literatura do produto pode precisar ser acompanhada.

## Criar um contêiner de blob, carregar um arquivo e configurar o acesso.

1. Na sua conta de armazenamento, localize a folha **Armazenamento de dados**.

1. Selecione **Contêineres** e, em seguida, selecione **+ Contêiner**.

1. Forneça um **nome** para seu novo contêiner,
2. **público**. Este é o armazenamento para o site público.

1. Defina o nível de acesso para **Contêiner (acesso de leitura anônimo para contêineres e blobs)**. Descreva brevemente os níveis de acesso. Isso é abordado com mais detalhes na última demonstração. 

1. Selecione **Criar**.

1. Aguarde até que o contêiner seja implantado e continue o trabalho no contêiner **público**.

1. **Carregar um blob**. Se tiver tempo, discuta as opções. 

1. Selecione o **arquivo carregado** e **copie a URL**.

1. Abra uma **nova guia do navegador**, cole a URL e verifique se o arquivo carregado é exibido.

1. Volte para o contêiner **público** e **Mude o nível de acesso** para **Privado (sem acesso anônimo)**.

1. **Atualize a guia URL** e confirme se o acesso ao recurso foi **negado**.

## Configure o gerenciamento do ciclo de vida.

1. [Slide de apoio] Comece com uma discussão sobre o gerenciamento do ciclo de vida. O grupo de marketing tem literatura de produtos que é sazonal. Por exemplo, a linha de roupas e acessórios de inverno. Este conteúdo pode ser arquivado até a próxima temporada. O arquivamento de conteúdo é fácil de realizar com uma regra de gerenciamento do ciclo de vida. Saiba mais, [Políticas de gerenciamento do ciclo de vida de blobs](https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview).

1. Continue trabalhando na conta de armazenamento.

1. Na folha **Gerenciamento de dados**, selecione **Gerenciamento do ciclo de vida**.

1. Na guia **Detalhes**, nomeie a regra **movetoarchive**.

1. Discuta o **escopo da regra** e como você pode **limitar blobs com filtros**. Por exemplo, mover apenas o conteúdo no contêiner específico.

1. Passe para a guia **Blobs de base**.

1. Discuta como a regra moverá automaticamente os blobs com base na última modificação ou criação há mais de dias.

1. Abra a lista suspensa **Em seguida** e discuta as opções. Tente dar exemplos com base em nosso cenário de laboratório. Por exemplo, o departamento de TI pode querer que os blobs sejam excluídos após 30 dias porque é uma conta de teste.

## Configure o acesso limitado ao conteúdo.

1. Analise os casos de uso para acesso limitado. Por exemplo, o conteúdo corporativo precisa ser compartilhado com fornecedores ou parceiros de terceiros. O acesso pode ser limitado a um período de tempo e ação específicos (ler, gravar). Saiba mais, [Assinaturas de acesso compartilhado](https://learn.microsoft.com/azure/storage/common/storage-sas-overview).

1. Continue com a **conta de armazenamento**.

1. Na folha **Segurança + rede**, selecione **Assinatura de acesso compartilhado**.

1. Revise os **tipos de Serviços permitidos** e **Recursos permitidos**. Explique que uma SAS pode ter como escopo uma conta de armazenamento, contêiner, arquivo ou arquivo de blob individual.

1. Revise as **Permissões permitidas**.

1. Selecione **Blob e Contêiner** e **Ler**.

1. Revise as configurações **Data/hora de início** e de **expiração**.

1. Selecione **Gerar a cadeia de conexão e de SAS**.

1. **Salve** as alterações. 

1. Copie a **URL SAS do serviço Blob** para uma nova guia do navegador.

1. Discuta como o conteúdo é exibido mesmo que este seja um contêiner privado.

## Configurar a replicação de objetos de blob. 

1. [Slide de apoio] Antes de continuar a demonstração, revise os casos de uso para replicação de objeto de blob. Por exemplo, é necessário fazer backup do conteúdo do site público. Explique que as contas de armazenamento podem estar em diferentes regiões do Azure, mas isso não é necessário. Saiba mais, [Replicação de objetos](https://learn.microsoft.com/azure/storage/blobs/object-replication-overview).

1. Crie uma **nova**conta de armazenamento.

1. **Crie** um **contêiner**, **backup**, na conta de armazenamento.

1. Retorne à primeira conta de armazenamento e ao contêiner **público**. 

1. Na folha **Gerenciamento de dados**, selecione **Replicação de objetos**.

1. Selecione **Criar regras de replicação**.

    - Conta de armazenamento de destino: a sua segunda conta de armazenamento

    - Contêiner de origem: **público**

    - Contêiner de destino: **backup**

1. **Crie** a regra. Explique que pode levar de 5 a 10 minutos para que o contêiner de origem seja replicado. Explique que os alunos terão esse tempo durante o laboratório. 

> **Observação**: os alunos agora conseguirão completar o LAB_02a e LAB_02b. 

  
