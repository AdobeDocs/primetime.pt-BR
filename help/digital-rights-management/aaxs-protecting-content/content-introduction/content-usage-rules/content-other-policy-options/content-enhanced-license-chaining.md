---
title: Encadeamento de licenças aprimorado
description: Encadeamento de licenças aprimorado
copied-description: true
exl-id: 5553f055-903f-4140-a425-08f21e8bce87
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Encadeamento de licenças aprimorado {#enhanced-license-chaining}

Permite que uma licença seja atualizada usando uma licença raiz pai para atualização em lote de licenças.

O Adobe Access 2.0 suportou encadeamento de licenças em que as licenças folha e raiz estão vinculadas a uma máquina específica. O Adobe Access 3.0 é compatível com o encadeamento aprimorado de licenças, no qual uma folha é vinculada a uma licença raiz e somente a licença raiz é vinculada a uma máquina ou domínio específico. O encadeamento de licenças aprimorado é compatível com a incorporação de licenças folha ao conteúdo, e o cliente só precisa adquirir a licença raiz do servidor de licenças para consumir o conteúdo protegido.

Para habilitar o encadeamento avançado de licenças, uma chave de criptografia raiz é atribuída à política. A chave de criptografia raiz é usada para vincular criptograficamente a licença folha à licença raiz.

>[!NOTE]
>
>O encadeamento aprimorado de licenças é suportado pelos clientes Adobe Access versão 3.0 e superior. Se um cliente mais antigo solicitar uma licença para conteúdo que ofereça suporte ao encadeamento de licenças aprimorado, o servidor de licenças ainda poderá emitir uma licença para esse cliente usando o encadeamento de licenças suportado pelo Adobe Access 2.0.

Exemplo de caso de uso: use essa opção para atualizar qualquer licença vinculada baixando uma única licença raiz. Por exemplo, implemente modelos de assinatura em que o conteúdo possa ser reproduzido, desde que o usuário renove a assinatura mensalmente. O benefício dessa abordagem é que os usuários só precisam fazer uma única aquisição de licença para atualizar todas as suas licenças de assinatura.
