---
seo-title: Atualizando políticas
title: Atualizando políticas
uuid: f6686c8b-bedf-4ec5-a14e-f03326519f89
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Atualizando políticas {#updating-policies}

Se as políticas forem atualizadas depois que o conteúdo for empacotado, forneça as políticas atualizadas ao servidor de licenças para que a versão atualizada possa ser usada ao emitir uma licença. Se o servidor de licenças tiver acesso a um banco de dados para armazenar políticas, você poderá recuperar a política atualizada do banco de dados e chamar `LicenseRequestMessage.setSelectedPolicy()` para fornecer a nova versão da política.

Para servidores de licença que não dependem de um banco de dados central, o SDK fornece suporte para Listas de Atualização de Política. Uma lista de atualização de política é um arquivo que contém uma lista de políticas atualizadas ou revogadas. Quando uma política for atualizada, gere uma nova Lista de Atualização de política e envie periodicamente a lista para fora de todos os servidores de licença. Passe a lista para o SDK definindo `HandlerConfiguration.setPolicyUpdateList()`. Se uma lista de atualização for fornecida, o SDK consultará essa lista ao analisar os metadados do conteúdo. `ContentInfo.getUpdatedPolicies()` contém as versões atualizadas das políticas especificadas nos metadados.

Consulte [Trabalhando com Políticas](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) e [listas de atualização de políticas.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
