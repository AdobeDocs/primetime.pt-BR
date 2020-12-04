---
seo-title: Trabalhar com o Lista de Atualização de Política
title: Trabalhar com o Lista de Atualização de Política
uuid: 583abb31-5c80-43f2-bc3d-a2300f61c4ea
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Trabalhar com o Lista{#working-with-policy-update-lists} de Atualização de Política

Para os servidores de licença que não têm acesso a um banco de dados para armazenar informações sobre políticas, você pode usar uma lista de atualização de política para notificar o servidor de licenças sobre políticas atualizadas. As Listas de Atualização de Política podem conter versões atualizadas de políticas ou uma lista de IDs de política que foram revogadas. Se uma lista de atualização de política for fornecida em `HandlerConfiguration`, o SDK imporá essa lista ao emitir uma licença.

As políticas também podem ser revogadas se os proprietários ou distribuidores de conteúdo desejarem interromper a emissão de licenças em uma política específica. Uma lista de atualização de política pode ser usada para aplicar a revogação de política no SDK. As listas de atualização de política também podem ser usadas para fornecer uma lista de políticas atualizadas ao SDK. Observe que revogar uma política não revoga licenças que já foram emitidas. Só impede a emissão de licenças adicionais no âmbito dessa política.

Trabalhar com listas de atualização de política envolve o uso de um objeto `PolicyUpdateListFactory`. Para criar uma lista de atualização de política, carregar uma lista de atualização de política existente e verificar se uma política foi atualizada ou revogada usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em Configurando o ambiente de desenvolvimento dentro do seu projeto.
1. Crie uma instância `ServerCredentialFactory` para carregar as credenciais necessárias para assinatura.
1. Crie uma instância `PolicyUpdateListFactory` usando o `ServerCredential` que você criou.
1. Especifique a ID de política a ser revogada.
1. Crie um objeto `PolicyRevocationEntry` usando a ID de política `String` que você acabou de criar e adicione-o à lista de atualização de política transmitindo-a para `PolicyUpdateListFactory.addRevocationEntry()`. Gere a nova lista de atualização de política chamando `PolicyUpdateListFactory.generatePolicyUpdateList()`. Da mesma forma, políticas atualizadas podem ser adicionadas à lista usando `PolicyUpdateEntry`.
1. Se uma lista de atualização de política já existir, você poderá serializá-la para carregamento chamando `PolicyUpdateList.getBytes()`. Para carregar a lista, chame `PolicyUpdateListFactory.loadPolicyUpdateList()` e passe na lista serializada.
1. Verifique se a assinatura é válida e se a lista foi assinada pelo certificado correto do servidor de licenças, ligando para `PolicyUpdateList.verifySignature()`.
1. Para verificar se uma entrada foi revogada, passe a ID da política `String` para `PolicyUpdateList.isRevoked()`. Como alternativa, a lista pode ser passada para `HandlerConfiguration` e será aplicada quando as licenças forem emitidas.

Para adicionar entradas adicionais a um `PolicyUpdateList` existente, carregue uma lista de atualização de política existente. Crie uma nova instância `PolicyUpdateListFactory`. Chame P `olicyUpdateListFactory.addEntries` para adicionar todas as entradas da lista antiga à nova lista. Chame `PolicyUpdateListFactory.addRevocationEntry` ou `addUpdatedEntry` para adicionar novas entradas de revogação ou atualização à PolicyUpdateList.

Para obter um exemplo de código demonstrando como criar uma lista de atualização de política, carregar uma lista de atualização de política existente e verificar se uma política foi revogada, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` no diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência.
