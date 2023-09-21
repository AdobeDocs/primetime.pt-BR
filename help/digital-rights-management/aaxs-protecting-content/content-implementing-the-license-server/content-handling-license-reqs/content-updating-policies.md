---
title: Atualização de políticas
description: Atualização de políticas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Atualização de políticas {#updating-policies}

Se as políticas forem atualizadas depois que o conteúdo for empacotado, forneça as políticas atualizadas ao servidor de licenças para que a versão atualizada possa ser usada ao emitir uma licença. Se o servidor de licença tiver acesso a um banco de dados para armazenar políticas, você poderá recuperar a política atualizada do banco de dados e chamar `LicenseRequestMessage.setSelectedPolicy()` para fornecer a nova versão da política.

Para servidores de licença que não dependem de um banco de dados central, o SDK fornece suporte para Listas de atualização de política. Uma lista de atualização de política é um arquivo que contém uma lista de políticas atualizadas ou revogadas. Quando uma política for atualizada, gere uma nova Lista de atualização de políticas e periodicamente a lista é enviada para todos os servidores de licença. Passar a lista para o SDK configurando `HandlerConfiguration.setPolicyUpdateList()`. Se uma lista de atualização for fornecida, o SDK consultará essa lista ao analisar os metadados de conteúdo. `ContentInfo.getUpdatedPolicies()` contém as versões atualizadas das políticas especificadas nos metadados.

Consulte [Trabalhar Com Políticas](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) e [Listas de atualização de política.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
