---
title: Encadeamento de licenças aprimorado
description: Encadeamento de licenças aprimorado
copied-description: true
exl-id: 269e7866-fe43-45a8-84d8-c51e4fc95f77
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Encadeamento de licenças aprimorado {#enhanced-license-chaining}

Você pode usar o encadeamento avançado de licenças para atualizar uma licença usando uma licença raiz pai para a atualização em lote de licenças.

O Primetime DRM 2.0 oferece suporte ao encadeamento de licenças, no qual as licenças folha e raiz estão vinculadas a uma máquina específica. O Primetime DRM 3.0 e superior oferece suporte a encadeamento de licenças aprimorado, no qual uma folha é vinculada a uma licença raiz e somente a licença raiz é vinculada a uma máquina ou domínio específico. O encadeamento de licenças aprimorado é compatível com a incorporação de uma licença folha ao conteúdo, e o cliente só precisa adquirir a licença raiz do servidor de licenças para consumir o conteúdo protegido.

Se quiser ativar o encadeamento avançado de licenças, atribua uma chave de criptografia raiz a uma política DRM do Primetime. A chave de criptografia raiz é usada para vincular criptograficamente a licença folha à licença raiz.

>[!NOTE]
>
>O encadeamento de licenças aprimorado é suportado pelos clientes DRM do Primetime versão 3.0 ou posterior. Se um cliente mais antigo solicitar uma licença para conteúdo compatível com o encadeamento de licenças aprimorado, o servidor de licenças ainda poderá emitir uma licença para esse cliente usando o encadeamento de licenças compatível com o Primetime DRM 2.0.

Exemplo de caso de uso: use essa opção para atualizar qualquer licença vinculada baixando uma única licença raiz. Por exemplo, implemente modelos de assinatura em que o conteúdo possa ser reproduzido, desde que o usuário renove a assinatura mensalmente. O benefício dessa abordagem é que os usuários só precisam adquirir uma única licença para atualizar todas as suas licenças de assinatura.
