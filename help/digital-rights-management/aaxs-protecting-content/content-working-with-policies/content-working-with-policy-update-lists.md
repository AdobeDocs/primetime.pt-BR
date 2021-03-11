---
title: Trabalhando com Listas de Atualização de Política
description: Trabalhando com Listas de Atualização de Política
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Trabalhando com Listas de Atualização de Política{#working-with-policy-update-lists}

Para servidores de licenças que não têm acesso a um banco de dados para armazenar informações sobre políticas, você pode usar uma lista de atualização de política para notificar o servidor de licenças sobre políticas atualizadas. As Listas de Atualização de Política podem conter versões atualizadas das políticas ou uma lista de IDs de política que foram revogadas. Se uma lista de atualização de política for fornecida em `HandlerConfiguration`, o SDK aplicará essa lista ao emitir uma licença.

As políticas também podem ser revogadas se os proprietários ou distribuidores de conteúdo quiserem interromper a emissão de licenças ao abrigo de uma política específica. Uma lista de atualização de política pode ser usada para aplicar a revogação de política no SDK. As listas de atualização de políticas também podem ser usadas para fornecer uma lista de políticas atualizadas ao SDK. Observe que revogar uma política não revoga licenças que já foram emitidas. Só impede a emissão de licenças adicionais no âmbito dessa política.

Trabalhar com listas de atualização de política envolve o uso de um objeto `PolicyUpdateListFactory`. Para criar uma lista de atualização de política, carregar uma lista de atualização de política existente e verificar se uma política foi atualizada ou revogada usando a API do Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em Configuração do ambiente de desenvolvimento em seu projeto.
1. Crie uma instância `ServerCredentialFactory` para carregar as credenciais necessárias para assinatura.
1. Crie uma instância `PolicyUpdateListFactory` usando o `ServerCredential` que você criou.
1. Especifique a ID de política a ser revogada.
1. Crie um objeto `PolicyRevocationEntry` usando a ID de política `String` que acabou de criar e adicione-o à lista de atualização de política ao passá-lo para `PolicyUpdateListFactory.addRevocationEntry()`. Gere a nova lista de atualização de política chamando `PolicyUpdateListFactory.generatePolicyUpdateList()`. Da mesma forma, políticas atualizadas podem ser adicionadas à lista usando `PolicyUpdateEntry`.
1. Se uma lista de atualização de política já existir, você poderá serializá-la para carregar, chamando `PolicyUpdateList.getBytes()`. Para carregar a lista, chame `PolicyUpdateListFactory.loadPolicyUpdateList()` e passe na lista serializada.
1. Verifique se a assinatura é válida e se a lista foi assinada pelo certificado correto do servidor de licenças ao chamar `PolicyUpdateList.verifySignature()`.
1. Para verificar se uma entrada foi revogada, passe o ID da política `String` para `PolicyUpdateList.isRevoked()`. Como alternativa, a lista pode ser passada para `HandlerConfiguration` e será aplicada quando as licenças forem emitidas.

Para adicionar mais entradas a um `PolicyUpdateList` existente, carregue uma lista de atualização de política existente. Crie uma nova instância `PolicyUpdateListFactory`. Chame P `olicyUpdateListFactory.addEntries` para adicionar todas as entradas da lista antiga à nova lista. Chame `PolicyUpdateListFactory.addRevocationEntry` ou `addUpdatedEntry` para adicionar novas entradas de revogação ou atualização à PolicyUpdateList.

Para obter um exemplo de código demonstrando como criar uma lista de atualização de política, carregar uma lista de atualização de política existente e verificar se uma política foi revogada, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` no diretório &quot;samples&quot; de Ferramentas de Linha de Comando de Implementação de Referência.
