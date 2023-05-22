---
title: Como Trabalhar com Listas de Atualização de Política DRM
description: Como Trabalhar com Listas de Atualização de Política DRM
copied-description: true
exl-id: 140f1fff-2078-427b-ade2-8ec18a14216f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Listas de atualização de política DRM {#drm-policy-update-lists}

Se você atualizar as regras de uso em uma política DRM depois de empacotar qualquer conteúdo, o servidor de licenças precisará ter a versão mais recente antes de poder emitir licenças que usam uma política DRM atualizada. Uma maneira de fazer isso é por meio de uma lista de atualização de política DRM.

Uma lista de atualização de política DRM é representada por um arquivo que inclui uma lista de políticas DRM atualizadas ou revogadas. Sempre que você atualiza uma política DRM, precisa gerar uma nova Lista de atualização de política DRM e enviar periodicamente a lista para todos os servidores de licença.

## Como Trabalhar com Listas de Atualização de Política DRM {#working-with-drm-policy-update-lists}

Para servidores de licença que não têm acesso a um banco de dados para armazenar informações sobre políticas DRM, é possível usar uma lista de atualização de política DRM para notificar o servidor de licença sobre políticas DRM atualizadas. As listas de atualização de política DRM podem incluir versões atualizadas de políticas DRM ou uma lista de IDs de política DRM que foram revogadas. Se uma lista de atualização de política estiver incluída em `HandlerConfiguration`, o SDK impõe essa lista ao emitir uma licença.

Você também pode revogar qualquer política de DRM se os proprietários ou distribuidores de conteúdo desejarem descontinuar a emissão de licenças de acordo com uma determinada política de DRM. Uma lista de atualização de política DRM pode ser usada para impor a revogação de política DRM no SDK. Também é possível aplicar listas de atualização de política DRM para fornecer uma lista de políticas DRM atualizadas ao SDK.

>[!NOTE]
>
>Sempre que você revoga uma política DRM, as licenças já emitidas não são automaticamente revogadas. Isso apenas impede que licenças adicionais sejam emitidas sob essa política de DRM.

## Atualizar Listas de Atualização de Política{#update-policy-update-lists}

O trabalho com listas de atualização de política DRM envolve o uso de um `PolicyUpdateListFactory` objeto. Para criar uma lista de atualização de política DRM, é necessário carregar uma lista de atualização de política DRM existente e verificar se uma política DRM foi atualizada ou revogada usando a API Java.

Para trabalhar com Listas de Atualização de Política DRM:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR incluídos ao configurar o ambiente de desenvolvimento em um projeto.
1. Criar um `ServerCredentialFactory` para carregar as credenciais necessárias para assinatura.
1. Criar um `PolicyUpdateListFactory` instância usando o `ServerCredential` criado.
1. Especifique a ID da política de DRM que deseja revogar.
1. Criar um `PolicyRevocationEntry` objeto usando a ID da política DRM `String` que você acabou de criar e, em seguida, adicioná-lo à lista de atualização de política DRM passando-o para `PolicyUpdateListFactory.addRevocationEntry()`.
1. Gerar a nova lista de atualização de política DRM chamando `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Da mesma forma, é possível atualizar as políticas de DRM para a lista usando `PolicyUpdateEntry`.
1. Se uma lista de atualização de política DRM já existir, você poderá serializá-la para carregamento chamando `PolicyUpdateList.getBytes()`.

   Para carregar a lista, chame `PolicyUpdateListFactory.loadPolicyUpdateList()` e passá-lo na lista serializada.
1. Verifique se a assinatura é válida e se a lista foi assinada pelo certificado correto do servidor de licenças, chamando `PolicyUpdateList.verifySignature()`.
1. Transmitir a ID da política DRM `String` em `PolicyUpdateList.isRevoked()` para verificar se uma entrada foi revogada.

   Como alternativa, você pode passar a lista para `HandlerConfiguration` em que é aplicada sempre que são emitidas licenças.
Se quiser adicionar mais entradas a um `PolicyUpdateList`, é necessário carregar uma lista de atualização de política DRM existente. Portanto, é necessário criar um novo DRM `PolicyUpdateListFactory` instância. Chame `PolicyUpdateListFactory.addEntries` para adicionar todas as entradas da lista antiga à nova lista. Chame `PolicyUpdateListFactory.addRevocationEntry` ou `addUpdatedEntry` para adicionar novas entradas de revogação ou atualização à PolicyUpdateList do DRM.

Para obter o código de exemplo que demonstra como criar uma lista de atualização de política DRM, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` no *Ferramentas de Linha de Comando de Implementação de Referência* [!DNL samples] diretório.
