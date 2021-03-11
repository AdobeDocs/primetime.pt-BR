---
title: Trabalhando com listas de atualização da política de DRM
description: Trabalhando com listas de atualização da política de DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Listas de atualização de política DRM {#drm-policy-update-lists}

Se você atualizar as regras de uso em uma política de DRM após empacotar qualquer conteúdo, o servidor de licenças precisará ter a versão mais recente para poder emitir licenças que usam uma política de DRM atualizada. Uma maneira de conseguir isso é através de uma lista de atualização da política de DRM.

Uma lista de atualização de política de DRM é representada por um arquivo que inclui uma lista de políticas de DRM atualizadas ou revogadas. Sempre que atualizar uma política de DRM, é necessário gerar uma nova Lista de atualização de política de DRM e enviar periodicamente a lista para todos os servidores de licença.

## Trabalhando com listas de atualização da política de DRM {#working-with-drm-policy-update-lists}

Para servidores de licenças que não têm acesso a um banco de dados para armazenar informações sobre políticas de DRM, convém usar uma lista de atualização de política de DRM para notificar o servidor de licenças sobre quaisquer políticas de DRM atualizadas. As Listas de Atualização de Política de DRM podem incluir versões atualizadas das políticas de DRM ou uma lista de IDs de política de DRM que foram revogadas. Se uma lista de atualização de política for incluída em `HandlerConfiguration`, o SDK aplica essa lista quando emite uma licença.

Você também pode revogar quaisquer políticas de DRM se os proprietários ou distribuidores de conteúdo quiserem interromper a emissão de licenças ao abrigo de uma política de DRM específica. Uma lista de atualização da política de DRM pode ser usada para aplicar a revogação da política de DRM no SDK. Também é possível aplicar listas de atualização da política de DRM para fornecer uma lista de políticas de DRM atualizadas ao SDK.

>[!NOTE]
>
>Sempre que você revogar uma política de DRM, as licenças que já foram emitidas não serão automaticamente revogadas. Apenas impede a emissão de licenças adicionais ao abrigo dessa política de DRM.

## Atualizar Listas de Atualização de Política{#update-policy-update-lists}

Trabalhar com listas de atualização de política de DRM envolve o uso de um objeto `PolicyUpdateListFactory`. Se quiser criar uma lista de atualização da política de DRM, é necessário carregar uma lista de atualização da política de DRM existente e verificar se uma política de DRM foi atualizada ou revogada usando a API Java.

Para trabalhar com as Listas de Atualização da Política DRM:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR incluídos ao configurar o ambiente de desenvolvimento em um projeto .
1. Crie uma instância `ServerCredentialFactory` para carregar as credenciais necessárias para assinatura.
1. Crie uma instância `PolicyUpdateListFactory` usando o `ServerCredential` que você criou.
1. Especifique a ID da política de DRM que deseja revogar.
1. Crie um objeto `PolicyRevocationEntry` usando o ID da política de DRM `String` que acabou de criar e adicione-o à lista de atualização da política de DRM, passando-o para `PolicyUpdateListFactory.addRevocationEntry()`.
1. Gere a nova lista de atualização da política de DRM chamando `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Da mesma forma, é possível atualizar as políticas de DRM para a lista usando `PolicyUpdateEntry`.
1. Se uma lista de atualização de política de DRM já existir, você poderá serializá-la para carregamento ao chamar `PolicyUpdateList.getBytes()`.

   Para carregar a lista, chame `PolicyUpdateListFactory.loadPolicyUpdateList()` e passe-a na lista serializada.
1. Verifique se a assinatura é válida e se a lista foi assinada pelo certificado correto do servidor de licenças ao chamar `PolicyUpdateList.verifySignature()`.
1. Passe o ID da política de DRM `String` para `PolicyUpdateList.isRevoked()` para verificar se uma entrada foi revogada.

   Como alternativa, você pode passar a lista para `HandlerConfiguration`, onde ela é aplicada sempre que as licenças são emitidas.
Se quiser adicionar mais entradas a um `PolicyUpdateList` existente, é necessário carregar uma lista de atualização da política de DRM existente. Portanto, você precisa criar uma nova instância de DRM `PolicyUpdateListFactory`. Chame `PolicyUpdateListFactory.addEntries` para adicionar todas as entradas da lista antiga à nova lista. Chame `PolicyUpdateListFactory.addRevocationEntry` ou `addUpdatedEntry` para adicionar novas entradas de revogação ou atualização à PolicyUpdateList de DRM.

Para obter um código de amostra que demonstra como criar uma lista de atualização de política de DRM, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` no diretório *Ferramentas de Linha de Comando de Implementação de Referência* [!DNL samples].
