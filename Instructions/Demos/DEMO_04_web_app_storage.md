---
demo:
  title: 'Demonstração 04: criar e configurar criptografia e acesso seguro ao aplicativo'
  module: Guided Project - Azure Files and Azure Blobs
--- 

## Demonstração – Criar e configurar criptografia e acesso seguro ao aplicativo. 

Nesta demonstração, explore a criptografia e a segurança do aplicativo.

> **Observação:** nesta demonstração, você criará uma identidade gerenciada, um cofre de chaves e uma chave. Para economizar tempo, convém pré-criar esses recursos. 

## Criar um cofre de chaves, uma chave e uma identidade gerenciada.

1. Crie uma nova conta de armazenamento do Azure. Ela será usada para mostrar recursos seguros de armazenamento.

1. [Slide de apoio] Antes de começar, revise como o novo aplicativo de desenvolvedor deve acessar com segurança o armazenamento de que precisa. O aplicativo é acessado por uma identidade gerenciada. A identidade gerenciada usa uma chave de criptografia armazenada no Azure Key Vault. O Azure Key Vault é um serviço de nuvem usado para gerenciar chaves, segredos e certificados. Esse processo substitui a necessidade de armazenar informações de segurança no código do aplicativo.  Nem todos os alunos podem estar familiarizados com esses conceitos.

1. Crie uma **identidade gerenciada**. Saiba mais, [Identidades gerenciadas](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview).

1. Crie um **cofre de chaves** com os padrões. Saiba mais, [Azure Key Vault](https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).

1. Aguarde até o cofre de chaves ser implantado e clique em **Ir para o recurso**.

1. Na folha **Objetos**, indique as **Chaves, Segredos e Certificados**.

1. Selecione **Chaves** e, em seguida, **Gerar/Importar**.

1. Dê um **nome** à chave e, em seguida, **Crie** a chave. Aceite os padrões.

## Configurar a conta de armazenamento para a identidade gerenciada e o cofre de chaves, atribuir permissões.

1. Volte para a conta de armazenamento.

1. Na folha **Segurança + Rede**, selecione **Criptografia**.

    - Selecione **Chaves gerenciadas pelo cliente**. Discuta a diferença entre uma chave gerenciada pela Microsoft e chaves gerenciadas pelo cliente. Por exemplo, uma chave gerenciada pela Microsoft é usada para criptografia e descriptografia de armazenamento automática. Uma chave gerenciada pelo cliente pode ser usada por um aplicativo. Saiba mais, [Chaves gerenciadas pelo cliente](https://learn.microsoft.com/azure/storage/common/customer-managed-keys-overview).

    - Em **tipo de armazenamento de chaves**, selecione **cofre de chaves**. As chaves podem ser armazenadas em software (cofre de chaves) ou em hardware (módulo de segurança de hardware). Estamos usando o cofre de chaves.

    - Selecione o seu **cofre de chaves** e **chave**.

    - Em **tipo de Identidade**, selecione uma **identidade gerenciada atribuída pelo sistema**. Esse é o padrão que configura a identidade gerenciada para que ela possa acessar o cofre de chaves.

1. [Slide de apoio] Neste ponto, você concedeu à identidade gerenciada acesso ao cofre de chaves e associou a identidade à conta de armazenamento. Agora, precisamos dar à identidade gerenciada acesso à conta de armazenamento. Saiba mais, [Atribuições de função do Azure](https://learn.microsoft.com/azure/role-based-access-control/role-assignments).

1. Volte para a conta de armazenamento e selecione **Controle de acesso (IAM)**. Saiba mais, [Funções internas do Azure](https://learn.microsoft.com/azure/role-based-access-control/built-in-roles).

    - Selecione **Adicionar** e, em seguida, **Adicionar atribuição de função**. Na guia **Tipo de atribuição**, indique que estamos atribuindo uma função de cargo.

    - Vá para a guia **Função** e procure **blob**. Selecione a função **Leitor de Dados de blob de armazenamento**.

    - Vá para a guia **Membros** e atribua acesso à **Identidade gerenciada**.

    - Selecione **Selecionar membros** e selecione a sua **identidade gerenciada atribuída pelo usuário**

## Configurar o armazenamento imutável.

1. [Slide de apoio] Os desenvolvedores precisam armazenar dados críticos para os negócios que não podem ser modificados ou excluídos por um tempo especificado pelo usuário. O armazenamento imutável permite que você proteja seus dados de serem substituídos ou excluídos. Discuta as políticas de retenção baseadas em tempo e as políticas de retenção legal. Saiba mais, [Armazenamento imutável](https://learn.microsoft.com/azure/storage/blobs/immutable-storage-overview).

1. Na sua **conta de armazenamento**, selecione a folha **Contêiner**.

1. **Crie** um contêiner chamado **hold** e **carregue** um arquivo.

1. Acesse seu contêiner **hold** e selecione a folha **Política de acesso**.

1. Na seção **Armazenamento de blobs imutável**, selecione **+ Adicionar política**.

1. Em **Tipo de política**, selecione **retenção baseada em tempo**.

1. Defina o **Período de retenção** como **5 dias**.

1. Não se esqueça de **Salvar** suas alterações.

1. Tente remover o arquivo pelo contêiner.

1. Verifique se não é possível excluir o arquivo devido à política.

## Configurar um escopo de criptografia para criptografia de infraestrutura.

1. Os desenvolvedores também precisam definir o escopo da criptografia de infraestrutura no nível do contêiner. Discuta escopos de criptografia e criptografia de infraestrutura. Saiba mais, [Escopos de criptografia](https://learn.microsoft.com/azure/storage/blobs/encryption-scope-overview).

1. Continue na **conta de armazenamento**.

1. Na seção **Segurança + Rede**, selecione **Criptografia**.

1. Vá para a guia **Escopo de criptografia** e selecione **+ Adicionar**.

1. Dê um **nome** ao **escopo de criptografia**.

1. Verifique se a **Criptografia de infraestrutura** está **habilitada**. Aponet a observação: "Esta opção não poderá ser alterada depois que esse escopo de criptografia for criado".

>**Observação**: os alunos agora conseguirão concluir o LAB_04. 
