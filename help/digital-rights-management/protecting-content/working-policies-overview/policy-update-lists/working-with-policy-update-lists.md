---
seo-title: Trabalhar com o Lista de atualização de política DRM
title: Trabalhar com o Lista de atualização de política DRM
uuid: 41f89671-81c6-4d3d-ac31-9c2a1980517a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Listas de atualização da política DRM {#drm-policy-update-lists}

Se você atualizar as regras de uso em uma política de DRM depois de empacotar qualquer conteúdo, o servidor de licenças precisará ter a versão mais recente antes de poder emitir licenças que usam uma política de DRM atualizada. Uma maneira de conseguir isso é através de uma lista de atualização de política de DRM.

Uma lista de atualização de política de DRM é representada por um arquivo que inclui uma lista de políticas de DRM atualizadas ou revogadas. Sempre que atualizar uma política de DRM, é necessário gerar uma nova Lista de atualização de política de DRM e enviar periodicamente a lista para todos os servidores de licença.

## Trabalhando com o DRM Policy Update Lista {#working-with-drm-policy-update-lists}

Para os servidores de licença que não têm acesso a um banco de dados para armazenar informações sobre políticas de DRM, você pode usar uma lista de atualização de política de DRM para notificar o servidor de licença sobre quaisquer políticas de DRM atualizadas. As Listas de atualização de política de DRM podem incluir versões atualizadas de políticas de DRM ou uma lista de IDs de política de DRM que foram revogadas. Se uma lista de atualização de política for incluída em `HandlerConfiguration`, o SDK imporá essa lista quando emitir uma licença.

Você também pode revogar quaisquer políticas de DRM se os proprietários ou distribuidores de conteúdo quiserem interromper a emissão de licenças de acordo com uma política específica de DRM. Uma lista de atualização de política de DRM pode ser usada para aplicar a revogação de política de DRM no SDK. Você também pode aplicar listas de atualização de política de DRM para fornecer uma lista de políticas de DRM atualizadas ao SDK.

>[!NOTE]
>
>Sempre que você revogar uma política de DRM, as licenças que já foram emitidas não serão revogadas automaticamente. Só impede que licenças adicionais sejam emitidas no âmbito dessa política de DRM.

## Atualizar Listas de Atualização de Política{#update-policy-update-lists}

Trabalhar com listas de atualização de política de DRM envolve o uso de um objeto `PolicyUpdateListFactory`. Se quiser criar uma lista de atualização de política DRM, é necessário carregar uma lista de atualização de política DRM existente e verificar se uma política DRM foi atualizada ou revogada usando a API Java.

Para trabalhar com Listas de atualização de política de DRM:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR incluídos quando você configurar o ambiente de desenvolvimento em um projeto.
1. Crie uma instância `ServerCredentialFactory` para carregar as credenciais necessárias para assinatura.
1. Crie uma instância `PolicyUpdateListFactory` usando o `ServerCredential` que você criou.
1. Especifique a ID da política de DRM que deseja revogar.
1. Crie um objeto `PolicyRevocationEntry` usando a ID de política do DRM `String` que você acabou de criar e adicione-o à lista de atualização de política do DRM, transmitindo-a para `PolicyUpdateListFactory.addRevocationEntry()`.
1. Gere a nova lista de atualização da política DRM chamando `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Da mesma forma, você pode atualizar as políticas de DRM para a lista usando `PolicyUpdateEntry`.
1. Se já existir uma lista de atualização da política DRM, você poderá serializá-la para carregamento chamando `PolicyUpdateList.getBytes()`.

   Para carregar a lista, chame `PolicyUpdateListFactory.loadPolicyUpdateList()` e passe-a na lista serializada.
1. Verifique se a assinatura é válida e se a lista foi assinada pelo certificado correto do servidor de licenças, chamando `PolicyUpdateList.verifySignature()`.
1. Passe a ID da política de DRM `String` para `PolicyUpdateList.isRevoked()` para verificar se uma entrada foi revogada.

   Como alternativa, você pode passar a lista para `HandlerConfiguration`, onde é aplicada sempre que as licenças são emitidas.
Se quiser adicionar mais entradas a um `PolicyUpdateList` existente, é necessário carregar uma lista de atualização de política de DRM existente. Portanto, é necessário criar uma nova instância de DRM `PolicyUpdateListFactory`. Chame `PolicyUpdateListFactory.addEntries` para adicionar todas as entradas da lista antiga à nova lista. Chame `PolicyUpdateListFactory.addRevocationEntry` ou `addUpdatedEntry` para adicionar novas entradas de revogação ou atualização à PolicyUpdateList do DRM.

Para obter um exemplo de código que demonstra como criar uma lista de atualização de política DRM, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` no diretório *Ferramentas de Linha de Comando de Implementação de Referência* [!DNL samples].
