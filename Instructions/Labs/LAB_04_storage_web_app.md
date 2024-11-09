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
    - Vá para a guia **Criptografia**.
    - Marque a caixa para **Habilitar criptografia de infraestrutura**.
    - Observe o aviso, *Esta opção não poderá ser alterada após a criação dessa conta de armazenamento.*
    - Selecione **Examinar + criar**.
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
    - Certifique-se de que, na guia **Configuração de acesso**, **Controle de acesso baseado em função do Azure (recomendado)** esteja selecionado. 
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
    - **Crie** o escopo de criptografia.
    - Retorne à conta de armazenamento e crie um novo contêiner.
    - Observe que na página **Novo contêiner** há o **Nome** e o **Nível de acesso público**.
    - Observe que na seção **Avançado** você pode selecionar o ** Escopo de criptografia** que você criou e aplicá-lo a todos os blobs no contêiner. 


>**Observação**: para ter uma prática adicional, conclua o módulo [Proteger e isolar o acesso aos recursos do Azure usando grupos de segurança de rede e pontos de extremidade de serviço](https://learn.microsoft.com/training/modules/secure-and-isolate-with-nsg-and-service-endpoints/). O módulo tem uma área restrita na qual você pode obter mais prática na restrição do acesso ao armazenamento.

## Limpar os recursos

Se você estiver trabalhando com **sua própria assinatura** e tiver concluído esses laboratórios, reserve um minuto para excluir os recursos do laboratório. Isso garantirá que os recursos sejam liberados e que o custo seja minimizado. A maneira mais fácil de excluir os recursos do laboratório é excluir o grupo de recursos do laboratório. 

+ No portal do Azure, selecione o grupo de recursos, selecione **Excluir o grupo de recursos**, **Inserir o nome do grupo de recursos** e clique em **Excluir**.
+ Usar o Azure PowerShell, `Remove-AzResourceGroup -Name resourceGroupName`.
+ Usar a CLI, `az group delete --name resourceGroupName`.

## Estender seu aprendizado com o Copilot

O Copilot pode ajudar você em sua jornada de aprendizado. O Copilot pode oferecer informações técnicas básicas, etapas de alto nível, prós e contras, ajuda para solução de problemas, casos de uso, exemplos de codificação e muito mais. Para acessar o Copilot, abra um navegador Edge e escolha Copilot (canto superior direito). Reserve alguns minutos para experimentar essas solicitações.
+ O que é uma identidade gerenciada do Azure e como ela pode ser usada com o armazenamento do Azure?
+ Quais funções de RBAC (controle de acesso baseado em função) internas estão disponíveis para gerenciar o acesso ao Armazenamento do Azure. 
+ O que são chaves gerenciadas pelo cliente e como elas são usadas para o armazenamento do Azure?

## Saiba mais com treinamento individual

+ [Proteger e isolar o acesso aos recursos do Azure usando grupos de segurança de rede e pontos de extremidade de serviço](https://learn.microsoft.com/training/modules/secure-and-isolate-with-nsg-and-service-endpoints/). Neste módulo, você verá como usar pontos de extremidade de serviço de rede virtual para controlar o tráfego de rede entre os serviços do Azure.

## Principais aspectos a serem lembrados
+ O Azure tem funções de RBAC internas para o armazenamento do Azure. Essas funções incluem: Colaborador da Conta de Armazenamento, Proprietário dos Dados de Blob de Armazenamento e Colaborador de Compartilhamento com SMB de Dados de Arquivos.
+ Você pode usar a própria chave de criptografia para proteger os dados em sua conta de armazenamento. Quando você especifica uma chave gerenciada pelo cliente, essa chave é usada para proteger e controlar o acesso à chave que criptografa os dados. 
+ O armazenamento imutável garante que os dados não possam ser modificados ou excluídos por um intervalo especificado pelo usuário. Existem dois tipos de políticas imutáveis: baseadas em tempo e retenção legal.
+ A criptografia de infraestrutura pode ser habilitada para toda a conta de armazenamento ou para um escopo de criptografia dentro de uma conta. A criptografia de infraestrutura é recomendada para cenários em que a criptografia dupla de dados é necessária para requisitos de conformidade. 
