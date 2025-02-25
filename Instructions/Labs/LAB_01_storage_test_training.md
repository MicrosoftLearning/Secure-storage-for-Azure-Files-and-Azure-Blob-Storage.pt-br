---
lab:
  title: 'Exercício 01: fornecer armazenamento para teste e treinamento do departamento de TI'
  module: Guided Project - Azure Files and Azure Blobs
---

O departamento de TI precisa criar protótipos de diferentes cenários de armazenamento e treinar novos funcionários. O conteúdo não é importante o suficiente para ser copiado em backup e não precisa ser restaurado caso os dados sejam substituídos ou removidos. O ideal é ter uma configuração simples que possa ser alterada com facilidade.

## Diagrama de arquitetura
![Diagrama com uma conta de armazenamento](../Media/task-1.png)

## Tarefas de habilidades
- Criar uma conta de armazenamento. 
- Defina as configurações básicas de segurança e rede. 

## Instruções para o exercício

## Crie um grupo de recursos e uma conta de armazenamento.

1. Crie e implante um grupo de recursos para manter todos os seus recursos de projeto. Saiba mais sobre [grupos de recursos](https://learn.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal).
    - No portal do Azure, pesquise e selecione `Resource groups`.
    - Selecione **+ Criar**.
    - Dê um **nome** ao grupo de recursos. Por exemplo, `storagerg`.
    - Selecione uma **região**. Use essa região em todo o projeto. 
    - Selecione **Revisar e criar** para validar o grupo de recursos.
    - Selecione **Criar** para implantar o grupo de recursos.

1. Crie e implante uma conta de armazenamento para dar suporte a testes e treinamento. Saiba mais sobre os [tipos de contas de armazenamento](https://learn.microsoft.com/azure/storage/common/storage-account-overview#types-of-storage-accounts).
    - No portal do Azure, pesquise e selecione `Storage accounts`. 
    - Selecione **+ Criar**.
    - Na guia **Informações básicas**, selecione seu **Grupo de recursos**.
    - Forneça um **Nome da conta de armazenamento**. O nome da conta de armazenamento deve ser exclusivo no Azure. 
    - Defina o **Desempenho** como **Padrão**. 
    - Selecione **Examinar** e depois **Criar**. 
    - Aguarde até a conta de armazenamento ser criada e selecione **Ir para o recurso**.  

## Defina configurações simples na conta de armazenamento.

1. Os dados dessa conta de armazenamento não exigem alta disponibilidade nem durabilidade. O ideal é ter uma solução de armazenamento de menor custo. Saiba mais sobre a [redundância da conta de armazenamento](https://learn.microsoft.com/azure/storage/common/storage-redundancy#locally-redundant-storage).
    - Na sua conta de armazenamento, na seção **Gerenciamento de dados**, selecione a folha **Redundância**.
    - Selecione **LRS (armazenamento com redundância local)** na lista suspensa **Redundância**. 
    - Não se esqueça de **Salvar** suas alterações. 
    - Atualize a página e observe que o conteúdo existe apenas no local primário. 

1. A conta de armazenamento só deve aceitar solicitações de conexões seguras. Saiba mais sobre como [exigir a transferência segura em conexões seguras](https://learn.microsoft.com/azure/storage/common/storage-require-secure-transfer)
    - Na seção **Configurações**, selecione a folha **Configuração**.
    - Verifique se a **Transferência segura obrigatória** está **Habilitada**. 

1. Os desenvolvedores gostariam que a conta de armazenamento usasse pelo menos o TLS versão 1.2. Saiba mais sobre o [protocolo TLS](https://learn.microsoft.com//azure/storage/common/transport-layer-security-configure-minimum-version?tabs=portal).
    - Na seção **Configurações**, selecione a folha **Configuração**.
    - Verifique se a **Versão mínima do TLS** está definida como **Versão 1.2**.  


1. Até que o armazenamento seja necessário novamente, desabilite as solicitações na conta de armazenamento. Saiba mais sobre [como desabilitar chaves compartilhadas](https://learn.microsoft.com/azure/storage/common/shared-key-authorization-prevent?tabs=portal#disable-shared-key-authorization).
    - Na seção **Configurações**, selecione a folha **Configuração**.
    - Verifique se a opção **Permitir acesso à chave da conta de armazenamento** está **Desabilitada**.
    - Não se esqueça de **Salvar** suas alterações. 

1. Verifique se a conta de armazenamento permite o acesso público em todas as redes.  
    - Na seção **Segurança + rede**, selecione a folha **Rede**.
    - Verifique se a opção **Acesso à rede pública** está definida como **Habilitado em todas as redes**.
    - Não se esqueça de **Salvar** suas alterações. 

>**Observação**: para ter uma prática adicional, conclua o módulo [Criar uma conta do Armazenamento do Azure](https://learn.microsoft.com/training/modules/create-azure-storage-account/). O módulo tem uma área restrita na qual você pode praticar a criação de uma conta de armazenamento.

## Estender seu aprendizado com o Copilot

O Copilot pode ajudar você em sua jornada de aprendizado. O Copilot pode oferecer informações técnicas básicas, etapas de alto nível, prós e contras, ajuda para solução de problemas, casos de uso, exemplos de codificação e muito mais. Para acessar o Copilot, abra um navegador Edge e escolha Copilot (canto superior direito). Reserve alguns minutos para experimentar essas solicitações.
+ O que é uma conta de Armazenamento do Microsoft Azure? Quais tipos de contas de armazenamento do Azure estão disponíveis?
+ Crie uma tabela comparando os níveis de desempenho do armazenamento do Azure. Destaque seus principais recursos e casos de uso. 
+ Quais opções de redundância de armazenamento estão disponíveis? Quando devo usar cada opção?

## Saiba mais com treinamento individual

+ [Descreva os serviços de armazenamento do Azure](https://learn.microsoft.com/training/modules/describe-azure-storage-services/). Neste módulo, você irá comparar os serviços de armazenamento do Azure, descrever as camadas de armazenamento e descrever as opções de redundância.
+ [Criar uma conta de Armazenamento do Microsoft Azure](https://learn.microsoft.com/training/modules/create-azure-storage-account/). Neste módulo, você criará e configurará uma conta de armazenamento. 

## Principais aspectos a serem lembrados

Parabéns por concluir o laboratório. Aqui estão as principais lições desse laboratório. 
+ Uma conta de armazenamento do Azure é um contêiner com todos os seus objetos de dados do Armazenamento do Azure, incluindo blobs, arquivos, filas e tabelas.
+ O Armazenamento do Azure oferece diversos tipos de contas de armazenamento, Standard e Premium. Cada tipo é compatível com recursos diferentes e tem um modelo de preços próprio.
+ O Armazenamento do Azure sempre armazena várias cópias dos seus dados para protegê-los contra eventos planejados e não planejados.
+ Os modelos de redundância podem replicar dados nas regiões primária e secundária. 
