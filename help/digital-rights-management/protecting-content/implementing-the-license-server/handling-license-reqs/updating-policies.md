---
seo-title: Atualização de políticas DRM
title: Atualização de políticas DRM
uuid: 6f7a1432-88e4-499b-a008-6c8cf0e9c09b
translation-type: tm+mt
source-git-commit: d5986e9bc8689bf37abdf242a41aea5e768df754
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Atualização de políticas DRM {#updating-drm-policies}

Se as políticas de DRM forem atualizadas após o conteúdo ser empacotado, forneça as políticas de DRM atualizadas ao servidor de licenças para que a versão atualizada possa ser usada ao emitir uma licença. Se um servidor de licenças tiver acesso a um banco de dados para armazenar políticas de DRM, você poderá recuperar a política de DRM atualizada do banco de dados e chamar `LicenseRequestMessage.setSelectedPolicy()` para fornecer a nova versão da política de DRM.

Para servidores de licença que não dependem de um banco de dados central, o SDK fornece suporte para Listas de atualização de política de DRM. Uma lista de atualização de política de DRM é um arquivo que inclui uma lista de políticas de DRM atualizadas ou revogadas. Quando uma política de DRM for atualizada, gere uma nova Lista de atualização de política de DRM e envie periodicamente a lista para todos os servidores de licença. Passe a lista para o SDK definindo `HandlerConfiguration.setPolicyUpdateList()`. Se uma lista de atualização for fornecida, o SDK consultará essa lista ao analisar os metadados do conteúdo. `ContentInfo.getUpdatedPolicies()` inclui as versões atualizadas das políticas de DRM especificadas nos metadados.

Consulte [Trabalhar com Políticas DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) e [listas de atualização da política DRM](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)