---
title: Atualização de políticas DRM
description: Atualização de políticas DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Atualização de políticas DRM {#updating-drm-policies}

Se as políticas de DRM forem atualizadas depois que o conteúdo for empacotado, forneça as políticas de DRM atualizadas ao servidor de licenças para que a versão atualizada possa ser usada ao emitir uma licença. Se um servidor de licença tiver acesso a um banco de dados para armazenar políticas DRM, você poderá recuperar a política DRM atualizada do banco de dados e chamar `LicenseRequestMessage.setSelectedPolicy()` para fornecer a nova versão da política de DRM.

Para servidores de licença que não dependem de um banco de dados central, o SDK fornece suporte para Listas de Atualização de Política DRM. Uma lista de atualização de política DRM é um arquivo que inclui uma lista de políticas DRM atualizadas ou revogadas. Quando uma política de DRM é atualizada, gere uma nova Lista de atualização de política de DRM e envie periodicamente a lista para todos os servidores de licença. Passar a lista para o SDK configurando `HandlerConfiguration.setPolicyUpdateList()`. Se uma lista de atualização for fornecida, o SDK consultará essa lista ao analisar os metadados de conteúdo. `ContentInfo.getUpdatedPolicies()` inclui as versões atualizadas das políticas DRM especificadas nos metadados.

Consulte [Como Trabalhar com Políticas de DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) e [Listas de atualização de política DRM](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
