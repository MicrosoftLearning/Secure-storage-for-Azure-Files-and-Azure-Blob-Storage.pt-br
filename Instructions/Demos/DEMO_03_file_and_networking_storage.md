---
demo:
  title: 'Demonstração 03: criar e configurar arquivos e rede de armazenamento'
  module: Guided Project - Azure Files and Azure Blobs
--- 

## Demonstração – Criar e configurar arquivos e rede de armazenamento.

Nesta demonstração, explore o armazenamento de arquivos do Azure e a rede de armazenamento.

> **Observação:** nesta demonstração, você criará uma nova conta de armazenamento e uma rede virtual com sub-rede. Elas podem ser pré-criadas para economizar tempo. 

## Revisar Arquivos do Azure e criar uma conta de armazenamento especificamente para compartilhamentos de arquivos.

1. [Slide de apoio] Antes de iniciar a demonstração, discuta o que é o Armazenamento de Arquivos do Azure e como ele é diferente do Armazenamento de Blobs do Azure. Saiba mais, [Cenários para o Armazenamento do Azure](https://learn.microsoft.com/azure/storage/common/storage-introduction).

1. Acesse o **portal do Azure**.

1. Crie uma **nova** conta de Armazenamento do Azure. Essa conta será usada para atender aos requisitos de arquivos compartilhados.

1. [Slide de apoio] Em **Desempenho**, selecione **Premium**. 

1. Em **Tipo de conta Premium**, selecione **Compartilhamentos de arquivo**. Compartilhamento de arquivo Premium são para aplicativos de compartilhamento de arquivo empresariais ou de alto desempenho. Nosso requisito de cenário é para um compartilhamento de arquivo corporativo. 

1. Em **Redundância**, selecione Armazenamento **com redundância de zona**. Lembre aos alunos que isso é recomendado para cenários de alta disponibilidade e protege contra falhas no datacenter.

1. Vá para a guia **Proteção de dados**.

1. Mostre que **Habilitar exclusão temporária para compartilhamentos de arquivos** está **habilitado**

1. **Revise** e **crie** a conta de armazenamento.

## Configurar o compartilhamento de arquivo.

1. Continua na conta de armazenamento.

1. Na folha **Armazenamento de dados**, selecione **Compartilhamentos de arquivo**.

1. Selecione **Compartilhamento de arquivo** e dê um nome ao compartilhamento de arquivo, **finance**.

1. Discuta a **Capacidade provisionada** e como um compartilhamento de arquivo premium é cobrado pelo tamanho do compartilhamento provisionado, independentemente da capacidade utilizada. Se tiver tempo, discuta outras configurações. 

1. Discuta **Protocolo**, selecione **SMB**.

1. Selecione **Criar**.

## Defina as configurações de compartilhamento de arquivo e crie um instantâneo.

1. Selecione o compartilhamento de arquivo **finance**.

1. Revise as configurações na parte superior da página. Por exemplo, **Carregar** e **Alterar tamanho e desempenho**.

1. [Slide de suporte] Discuta a finalidade dos instantâneos. Saiba mais, [Instantâneos de compartilhamento de arquivo](https://learn.microsoft.com/azure/storage/files/storage-snapshots-files).

1. No painel **Operações**, selecione **Instantâneos**.

1. Selecione **Adicionar instantâneo** e **OK**. Adicionar um comentário é opcional.

1. Os alunos carregarão, capturarão instantâneos e restaurarão arquivos no laboratório.

## Configure acesso de rede para armazenamento.

1. [Slide de apoio] Antes de configurar a rede de armazenamento, discuta as várias opções. Revise algumas das opções de rede anteriores que foram configuradas. 

1. No portal, pesquise **redes virtuais**.

1. Use a guia **Noções básicas** para criar uma rede virtual chamada **corpnet**. Crie uma **sub-rede**, **finance**. Ressalte que essa rede já estaria criada.

1. Volte para a conta de armazenamento.

1. No painel **Segurança +rede**, selecione **Rede**.

1. Selecione **Habilitado a partir das redes virtuais e endereços IP selecionados**.

1. Na página **Adicionar rede**, adicione a rede virtual **corpnet** e a sub-rede **finance**.

1. **Habilite o ponto de extremidade**. Explique que um novo ponto de extremidade de serviço pode levar até 15 minutos para ser criado.

1. Revise as configurações de **Firewall**.

1. Revise a seção **Roteamento de Rede** e verifique se o roteamento de rede da Microsoft está sendo usado.



1. Se tiver tempo, faça uma demonstração rápida do **Navegador de armazenamento**. 

>**Observação**: os alunos agora conseguirão completar o LAB_03. 
