---
demo:
  title: 'Demonstração 01: criar e configurar contas de armazenamento'
  module: Guided Project - Azure Files and Azure Blobs
---
## Demonstração – Criar e configurar contas de armazenamento 

Nesta demonstração, explore as contas de armazenamento.

1. [Slide de apoio] Antes de começar esta demonstração, convém discutir como o armazenamento é organizado e os fatores a serem considerados. 

1. Acesse o **portal do Azure**.

1. Na caixa de pesquisa, digite **Contas de armazenamento**. Quando você começa a digitar, a lista é filtrada com base em sua entrada.

1. Selecione **Contas de Armazenamento**.

1. Selecione **Criar**.

1. Explique como o portal do Azure fornece uma interface de assistente fácil de usar. Lembre os alunos de que os itens marcados com um asterisco vermelho são obrigatórios.

1. Selecione a **assinatura**.

1. Selecione o **grupo de recursos**.

1. Insira um nome para a conta de armazenamento. Discuta as restrições de nomenclatura da conta de armazenamento.

1. Selecione uma região para sua conta de armazenamento. Analise qual região os alunos devem usar no laboratório. Saiba mais sobre as [geografias do Azure](https://azure.microsoft.com/explore/global-infrastructure/geographies/).

1. [Slide de apoio] Selecione o desempenho **padrão**. Saiba mais, [Tipos de contas de armazenamento](https://learn.microsoft.com/azure/storage/common/storage-account-overview).

1. [Slide de apoio] Selecione **Redundância** como armazenamento **localmente redundante**. Saiba mais, [Redundância do armazenamento do Azure](https://docs.microsoft.com/azure/storage/common/storage-redundancy).

1. Vá para a guia **Avançado**. Na seção **Segurança**, realce essas configurações. Estamos cobrindo apenas algumas coisas para introduzir o aluno ao seu primeiro laboratório. 

    - **Exigir transferência segura para operações da API REST**. Por padrão, as solicitações de contas de armazenamento só são aceitas por meio de conexão segura. Saiba mais, [Transferência segura](https://learn.microsoft.com/azure/storage/common/storage-require-secure-transfer).

    - **Habilitar o acesso à chave da conta de armazenamento**. Discuta como essa configuração pode desabilitar o acesso à conta de armazenamento. Por exemplo, o acesso à conta de armazenamento do departamento de TI pode ser desabilitado. Discuta a importância de proteger a chave. Saiba mais, [Gerenciar chaves de acesso da conta de armazenamento](https://learn.microsoft.com/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).

    - **Versão mínima do TLS**. Explique que o TLS é para proteger as comunicações na rede. O TLS é uma versão melhorada do SSL. Seus desenvolvedores podem perguntar quais versões estão disponíveis. Saiba mais, [Transport Layer Service](https://learn.microsoft.com/azure/storage/common/transport-layer-security-configure-minimum-version).

1. Explique que outras guias serão abordadas à medida que os alunos passarem pelos laboratórios.

1. Selecione **Revisar** e verifique se não há erros de validação. Discuta possíveis erros de validação. 

1. Selecione **Criar** e aguarde enquanto a conta de armazenamento é implantada. Aponte as mensagens de notificação.

1. Mostre como **Ir para o recurso**. Discuta outras formas de chegar ao recurso.

>**Observação**: os alunos conseguirão completar o LAB_01.
