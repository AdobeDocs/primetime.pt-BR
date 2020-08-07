---
seo-title: Aumento do encadeamento de licenças
title: Aumento do encadeamento de licenças
uuid: 5e4e825a-de84-4ab2-a652-02cc03153957
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Aumento do encadeamento de licenças {#enhanced-license-chaining}

Você pode usar o encadeamento aprimorado de licença para atualizar uma licença usando uma licença raiz pai para a atualização em lote de licenças.

O Primetime DRM 2.0 suporta encadeamento de licença no qual as licenças de folha e raiz estão vinculadas a uma máquina específica. O Primetime DRM 3.0 e superior tem suporte para encadeamento de licença aprimorado, no qual uma folha está vinculada a uma licença raiz, e somente a licença raiz está vinculada a uma máquina ou domínio específico. O encadeamento de licença aprimorado suporta a incorporação de uma licença de folha com o conteúdo, e o cliente só precisa adquirir a licença raiz do servidor de licença para consumir o conteúdo protegido.

Se você quiser ativar o encadeamento de licença aprimorado, é necessário atribuir uma chave de criptografia raiz a uma política de DRM Primetime. A chave de criptografia raiz é usada para vincular criptograficamente a licença de folha à licença raiz.

>[!NOTE]
>
>Os clientes Primetime DRM versão 3.0 ou posterior oferecem suporte para o encadeamento aprimorado de licenças. Se um cliente mais antigo solicitar uma licença para conteúdo compatível com o encadeamento de licença aprimorado, o servidor de licença ainda poderá emitir uma licença para esse cliente usando o encadeamento de licença compatível com o Primetime DRM 2.0.

Exemplo de caso de uso: Use esta opção para atualizar quaisquer licenças vinculadas baixando uma única licença raiz. Por exemplo, implemente modelos de subscrição nos quais o conteúdo pode ser reproduzido desde que o usuário renove a subscrição mensalmente. A vantagem desta abordagem é que os usuários só precisam adquirir uma única licença para atualizar todas as suas licenças de subscrição.
