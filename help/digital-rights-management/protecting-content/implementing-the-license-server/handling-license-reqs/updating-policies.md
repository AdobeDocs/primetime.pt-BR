---
title: Atualização das políticas de DRM
description: Atualização das políticas de DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Atualização das políticas de DRM {#updating-drm-policies}

Se as políticas de DRM forem atualizadas depois que o conteúdo for empacotado, forneça as políticas de DRM atualizadas ao servidor de licença para que a versão atualizada possa ser usada ao emitir uma licença. Se um servidor de licenças tiver acesso a um banco de dados para armazenar políticas de DRM, você poderá recuperar a política de DRM atualizada do banco de dados e chamar `LicenseRequestMessage.setSelectedPolicy()` para fornecer a nova versão da política de DRM.

Para servidores de licenças que não dependem de um banco de dados central, o SDK fornece suporte para Listas de atualização de políticas de DRM. Uma lista de atualização de política de DRM é um arquivo que inclui uma lista de políticas de DRM atualizadas ou revogadas. Quando uma política de DRM for atualizada, gere uma nova Lista de atualização de política de DRM e envie periodicamente a lista para todos os servidores de licença. Passe a lista para o SDK definindo `HandlerConfiguration.setPolicyUpdateList()`. Se uma lista de atualização for fornecida, o SDK consultará essa lista ao analisar os metadados de conteúdo. `ContentInfo.getUpdatedPolicies()` O inclui as versões atualizadas das políticas de DRM especificadas nos metadados.

Consulte [Trabalhar com políticas de DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) e [Listas de atualização de política de DRM](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)