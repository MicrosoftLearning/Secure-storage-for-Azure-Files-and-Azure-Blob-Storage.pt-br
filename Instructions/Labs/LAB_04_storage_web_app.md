---
lab:
  title: 'Exercício 04: fornecer armazenamento para um novo aplicativo da empresa'
  module: Guided Project - Azure Files and Azure Blobs
---
A empresa está projetando e desenvolvendo um novo aplicativo. Os desenvolvedores precisam garantir que o armazenamento seja acessado apenas usando chaves e identidades gerenciadas. Os desenvolvedores desejam usar o controle de acesso baseado em função. Para ajudar com o teste, é necessário ter um armazenamento imutável protegido. 

## Diagrama de arquitetura

![Diagrama com uma conta de armazenamento, identidades gerenciadas e um cofre de chaves.](../Media/task-5.png)

## Tarefas de habilidades

- Criar a conta de armazenamento e a identidade gerenciada.
- Proteger o acesso à conta de armazenamento com um cofre de chaves e uma chave.
- Configurar a conta de armazenamento para usar a chave gerenciada pelo cliente no cofre de chaves.
- Configurar uma política de retenção baseada em tempo e um escopo de criptografia.

## Instruções para o exercício

## Crie a conta de armazenamento e a identidade gerenciada

1. Forneça uma conta de armazenamento para o aplicativo Web. 
    - No portal do Azure, procure e selecione **Contas de armazenamento**. 
    - Selecione **+ Criar**.
    - Em **Grupo de recursos**, selecione **Criar novo**. Dê um **nome** ao grupo de recursos e selecione **OK** para salvar as alterações.
    - Forneça um **Nome da conta de armazenamento**. Garanta que o nome seja exclusivo e atenda aos requisitos de nomenclatura. 
    - **Revise** e **Crie** a conta de armazenamento.
    - Aguarde até o recurso ser implantado.

1. Forneça uma identidade gerenciada para o aplicativo Web usar.  Saiba mais sobre [identidades gerenciadas](https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).

    - Procure e selecione **Identidades gerenciadas**.
    - Selecione **Criar**.
        - Selecione o **grupo de recursos**. 
        - Dê um nome à identidade gerenciada.
    - Selecione **Revisar e Criar** e, em seguida, **Criar**. 

1. Atribua as permissões corretas à identidade gerenciada. A identidade só precisa ler e listar os contêineres e os blobs. Saiba mais sobre [como atribuir funções do Azure](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal).
    
    - Procure e selecione sua **conta de armazenamento**.
    - Selecione o painel **IAM (Controle de Acesso)**.
    - Selecione **Adicionar atribuição de função** (centro da página).
    - Na página **Funções de trabalho**, procure e selecione a função **Leitor de Dados do Blob de Armazenamento**. 
    - Na página **Membros**, selecione **Identidade gerenciada**.
    - Selecione **Selecionar membros**. Na lista suspensa **Identidade gerenciada**, selecione **Identidade gerenciada atribuída pelo usuário**.
    - Selecione a identidade gerenciada que você criou na etapa anterior. 
    - Clique em **Selecionar** e em **Revisar + atribuir** a função. 
    - Selecione **Revisar + atribuir** mais uma vez para adicionar a atribuição de função.
    - Sua conta de armazenamento agora pode ser acessada por uma identidade gerenciada com as permissões do Leitor de Dados do Blob de Armazenamento. 

## Proteger o acesso à conta de armazenamento com um cofre de chaves e uma chave

1. Para criar o cofre de chaves e a chave necessários para esta parte do laboratório, sua conta de usuário deve ter permissões de Administrador do Key Vault. Saiba mais sobre como [fornecer acesso a chaves, certificados e segredos do Key Vault com um controle de acesso baseado em função do Azure](https://learn.microsoft.com/azure/key-vault/general/rbac-guide?tabs=azure-cli)
    - No portal, pesquise e selecione **Grupos de recursos**. 
    - Selecione o **grupo de recursos** e, em seguida, selecione a folha **Controle de acesso (IAM)**.
    - Selecione **Adicionar atribuição de função** (centro da página).
    - Na guia **Funções de trabalho**, pesquise e selecione a função **Administrador do Key Vault**.
    - Na página **Membros**, selecione **Usuário, grupo ou entidade de serviço**.
    - Escolha **Selecionar membros**.
    - Procure sua conta de usuário e selecione-a. Sua conta de usuário é exibida no canto superior direito do portal.
    - Clique em **Selecionar** e em **Revisar + atribuir**.
    - Selecione **Revisar + atribuir** mais uma vez para adicionar a atribuição de função.
    - Agora você pode continuar o laboratório.

1. Crie um cofre de chaves para armazenar as chaves de acesso. 

    - No portal, procure e selecione **Cofres de chave**.
    - Selecione **Criar**.
    - Selecione o **grupo de recursos**.
    - Forneça o **nome** do cofre de chaves. O nome deve ser exclusivo.
    - Verifique na guia **Configuração de acesso** se a **Política de acesso ao cofre** está selecionada. 
    - Selecione **Examinar + criar**.
    - Aguarde as verificações de validação serem concluídas e selecione **Criar**.
    - Após a implantação, selecione **Acessar recurso**.
    - Na folha **Visão geral**, verifique se **Exclusão temporária** e **Proteção contra limpeza** estão **habilitadas**. 

1. Crie uma chave gerenciada pelo cliente no cofre de chaves. 

    - No **cofre de chaves**, na seção **Objetos**, selecione a folha **Chaves**.
    - Selecione **Gerar/Importar** e **dê um nome** à chave.
    - Use os valores padrão para o restante dos parâmetros e **Crie** a chave.

## Configurar a conta de armazenamento para usar a chave gerenciada pelo cliente no cofre de chaves.

1. Antes de concluir as próximas etapas, você deve atribuir a função Usuário do Serviço de Criptografia do Key Vault à identidade gerenciada. Saiba mais sobre como [usar uma identidade gerenciada atribuída pelo sistema para autorizar o acesso](https://learn.microsoft.com/azure/storage/common/customer-managed-keys-configure-existing-account?tabs=azure-portal#use-a-system-assigned-managed-identity-to-authorize-access)
    - No portal, pesquise e selecione **Grupos de recursos**. 
    - Selecione o **grupo de recursos** e, em seguida, selecione a folha **Controle de acesso (IAM)**.
    - Selecione **Adicionar atribuição de função** (centro da página).
    - Na página **Funções de trabalho**, procure e selecione a função **Usuário do Serviço de Criptografia do Key Vault**.
    - Na página **Membros**, selecione **Identidade gerenciada**.
    - Selecione **Selecionar membros**. Na lista suspensa **Identidade gerenciada**, selecione **Identidade gerenciada atribuída pelo usuário**.
    - Selecione sua identidade gerenciada.  
    - Clique em **Selecionar** e em **Revisar + atribuir**.
    - Selecione **Revisar + atribuir** mais uma vez para adicionar a atribuição de função.
    
1. Configurar a conta de armazenamento para usar a chave gerenciada pelo cliente no cofre de chaves. Saiba mais sobre as [chaves gerenciadas pelo cliente em uma conta de armazenamento existente](https://learn.microsoft.com/azure/storage/common/customer-managed-keys-configure-existing-account?WT.mc_id=Portal-Microsoft_Azure_Storage&tabs=azure-portal).
    - Retorne à sua conta de armazenamento.
    - Na seção **Segurança + rede**, escolha a folha **Criptografia**.
    - Selecione **Chaves gerenciadas pelo cliente**.
    - **Selecione um cofre de chaves e uma chave**. Selecione seu cofre de chaves e chave.
    - **Selecione** para confirmar suas escolhas. 
    - Verifique se o **Tipo de identidade** é **Atribuída pelo usuário**.
    - **Selecione uma identidade**.
    - Selecione sua identidade gerenciada e selecione **Adicionar**. 
    - **Salve** suas alterações.
    - Se você receber um erro informando que sua identidade não tem as permissões corretas, aguarde um minuto e tente novamente. 

## Configurar uma política de retenção baseada em tempo e um escopo de criptografia.

1. Os desenvolvedores exigem um contêiner de armazenamento em que os arquivos não possam ser modificados, mesmo pelo administrador. Saiba mais sobre o [armazenamento imutável de blobs](https://learn.microsoft.com/azure/storage/blobs/immutable-storage-overview).

    - Navegue até sua **conta de armazenamento**.
    - Na seção **Armazenamento de dados**, selecione a folha **Contêineres**. 
    - Crie o contêiner chamado **hold**. Aceite os padrões. Certifique-se de **Criar** o contêiner. 
    - Carregue um arquivo no contêiner. 
    - Na seção **Configurações**, selecione a folha **Política de acesso**. 
    - Na seção **Armazenamento de blobs imutável**, selecione **+ Adicionar política**. 
    - Em **Tipo de política**, selecione **retenção baseada em tempo**. 
    - Defina o **Período de retenção** como **5 dias**. 
    - Não se esqueça de **Salvar** suas alterações. 
    - Tente **remover** o arquivo no contêiner. 
    - Verifique se você recebeu uma notificação de **falha ao excluir blobs** devido à política.  

1. Os desenvolvedores exigem um escopo de criptografia que permita a criptografia de infraestrutura. Saiba mais sobre a [criptografia de infraestrutura](https://learn.microsoft.com/azure/storage/common/infrastructure-encryption-enable?tabs=portal).

    - Navegar de volta para sua conta de armazenamento. 
    - Na folha **Segurança + Rede**, selecione **Criptografia**.
    - Na guia **Escopos de criptografia**, selecione **Adicionar**.
    - Dê um **nome** ao escopo de criptografia. 
    - O **Tipo de criptografia** é **Chave gerenciada pela Microsoft**.
    - Defina a **criptografia de infraestrutura** como **Habilitar**.
    - Observe o aviso de que a habilitação da criptografia de infraestrutura não pode ser alterada após a criação do escopo.
    - **Crie** o escopo de criptografia.
    - Retorne à conta de armazenamento e crie um novo contêiner.
    - Observe que na página **Novo contêiner** há o **Nome** e o **Nível de acesso público**.
    - Observe que na seção **Avançado** você pode selecionar o ** Escopo de criptografia** que você criou e aplicá-lo a todos os blobs no contêiner. 


>**Observação**: para ter uma prática adicional, conclua o módulo [Proteger e isolar o acesso aos recursos do Azure usando grupos de segurança de rede e pontos de extremidade de serviço](https://learn.microsoft.com/training/modules/secure-and-isolate-with-nsg-and-service-endpoints/). O módulo tem uma área restrita na qual você pode obter mais prática na restrição do acesso ao armazenamento.
