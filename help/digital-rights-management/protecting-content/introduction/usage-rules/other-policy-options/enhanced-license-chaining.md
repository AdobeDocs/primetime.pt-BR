---
title: Cadeamento de licenças aprimorado
description: Cadeamento de licenças aprimorado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Cadeamento de licença aprimorado {#enhanced-license-chaining}

Você pode usar o encadeamento aprimorado de licenças para atualizar uma licença usando uma licença raiz pai para atualização em lote de licenças.

O Primetime DRM 2.0 oferece suporte ao encadeamento de licenças, no qual as licenças de folha e raiz estão vinculadas a uma máquina específica. O Primetime DRM 3.0 e superior tem suporte para encadeamento de licença aprimorado, em que uma folha é vinculada a uma licença raiz e somente a licença raiz é vinculada a uma máquina ou domínio específico. O encadeamento de licença aprimorado oferece suporte à incorporação de uma licença de folha com o conteúdo, e o cliente precisa apenas adquirir a licença de raiz do servidor de licença para consumir o conteúdo protegido.

Se quiser ativar o encadeamento aprimorado da licença, atribua uma chave de criptografia raiz a uma política de DRM do Primetime. A chave de criptografia raiz é usada para vincular criptograficamente a licença de folha à licença raiz.

>[!NOTE]
>
>O encadeamento aprimorado de licenças é suportado pelos clientes DRM do Primetime versão 3.0 ou posterior. Se um cliente mais antigo solicitar uma licença para conteúdo que suporte o encadeamento aprimorado de licenças, o servidor de licenças ainda poderá emitir uma licença para esse cliente usando o encadeamento de licenças compatível com o Primetime DRM 2.0.

Exemplo de caso de uso: Use esta opção para atualizar qualquer licença vinculada baixando uma única licença raiz. Por exemplo, implemente modelos de assinatura em que o conteúdo possa ser reproduzido, desde que o usuário renove a assinatura mensalmente. A vantagem dessa abordagem é que os usuários só precisam adquirir uma única licença para atualizar todas as licenças de assinatura.
