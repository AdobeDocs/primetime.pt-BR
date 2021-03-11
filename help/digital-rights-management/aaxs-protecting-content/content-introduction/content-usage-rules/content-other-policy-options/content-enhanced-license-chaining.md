---
title: Cadeamento de licenças aprimorado
description: Cadeamento de licenças aprimorado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Cadeamento de licença aprimorado {#enhanced-license-chaining}

Permite que uma licença seja atualizada usando uma licença raiz pai para atualização em lote de licenças.

O Adobe Access 2.0 oferece suporte ao encadeamento de licenças, no qual as licenças de folha e raiz estão vinculadas a uma máquina específica. O Adobe Access 3.0 tem suporte para encadeamento de licença aprimorado, no qual uma folha é vinculada a uma licença raiz e somente a licença raiz é vinculada a uma máquina ou domínio específico. O encadeamento de licença aprimorado oferece suporte à incorporação de licença de folha com o conteúdo, e o cliente só precisa adquirir a licença raiz do servidor de licença para consumir o conteúdo protegido.

Para ativar o encadeamento de licença aprimorado, uma chave de criptografia raiz é atribuída à política . A chave de criptografia raiz é usada para vincular criptograficamente a licença de folha à licença raiz.

>[!NOTE]
>
>O encadeamento aprimorado de licenças é compatível com os clientes do Adobe Access versão 3.0 e superior. Se um cliente mais antigo solicitar uma licença para conteúdo que ofereça suporte ao encadeamento aprimorado de licenças, o servidor de licenças ainda poderá emitir uma licença para esse cliente usando o encadeamento de licenças suportado pelo Adobe Access 2.0.

Exemplo de caso de uso: Use esta opção para atualizar qualquer licença vinculada baixando uma única licença raiz. Por exemplo, implemente modelos de assinatura em que o conteúdo possa ser reproduzido, desde que o usuário renove a assinatura mensalmente. O benefício dessa abordagem é que os usuários só precisam fazer uma única aquisição de licença para atualizar todas as licenças de assinatura.
