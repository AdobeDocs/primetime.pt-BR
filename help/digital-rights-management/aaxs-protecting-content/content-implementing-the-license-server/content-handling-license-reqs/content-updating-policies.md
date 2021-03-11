---
title: Atualização de políticas
description: Atualização de políticas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Atualizando políticas {#updating-policies}

Se as políticas forem atualizadas depois que o conteúdo for empacotado, forneça as políticas atualizadas ao servidor de licenças para que a versão atualizada possa ser usada ao emitir uma licença. Se o servidor de licenças tiver acesso a um banco de dados para armazenar políticas, você poderá recuperar a política atualizada do banco de dados e chamar `LicenseRequestMessage.setSelectedPolicy()` para fornecer a nova versão da política.

Para servidores de licenças que não dependem de um banco de dados central, o SDK fornece suporte para Listas de Atualização de Políticas. Uma lista de atualização de política é um arquivo que contém uma lista de políticas atualizadas ou revogadas. Quando uma política for atualizada, gere uma nova Lista de atualização de política e envie periodicamente a lista para todos os servidores de licença. Passe a lista para o SDK definindo `HandlerConfiguration.setPolicyUpdateList()`. Se uma lista de atualização for fornecida, o SDK consultará essa lista ao analisar os metadados de conteúdo. `ContentInfo.getUpdatedPolicies()` contém as versões atualizadas das políticas especificadas nos metadados.

Consulte [Trabalhando com políticas](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) e [Listas de atualização de políticas.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
