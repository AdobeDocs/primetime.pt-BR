---
title: Trabalhando com Listas de Atualização de Políticas
description: Trabalhando com Listas de Atualização de Políticas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Trabalhando com Listas de Atualização de Políticas{#working-with-policy-update-lists}

Para servidores de licença que não têm acesso a um banco de dados para armazenar informações sobre políticas, você pode usar uma lista de atualização de políticas para notificar o servidor de licença sobre políticas atualizadas. As Listas de Atualização de Política podem conter versões atualizadas de políticas ou uma lista de IDs de política que foram revogadas. Se uma lista de atualização de política for fornecida em `HandlerConfiguration`, o SDK aplicará essa lista ao emitir uma licença.

As políticas também podem ser revogadas se os proprietários ou distribuidores de conteúdo quiserem descontinuar a emissão de licenças de acordo com uma política específica. Uma lista de atualização de política pode ser usada para impor a revogação de política no SDK. As listas de atualização de política também podem ser usadas para fornecer uma lista de políticas atualizadas para o SDK. Observe que a revogação de uma política não revoga licenças que já foram emitidas. Apenas impede a emissão de licenças adicionais ao abrigo dessa política.

Trabalhar com listas de atualização de política envolve o uso de um `PolicyUpdateListFactory` objeto. Para criar uma lista de atualização de política, carregar uma lista de atualização de política existente e verificar se uma política foi atualizada ou revogada usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em Configuração do ambiente de desenvolvimento no seu projeto.
1. Criar um `ServerCredentialFactory` para carregar as credenciais necessárias para assinatura.
1. Criar um `PolicyUpdateListFactory` instância usando o `ServerCredential` você criou.
1. Especifique a ID da política a ser revogada.
1. Criar um `PolicyRevocationEntry` objeto usando a ID da política `String` você acabou de criar e adicioná-lo à lista de atualização de política transmitindo-o para `PolicyUpdateListFactory.addRevocationEntry()`. Gerar a nova lista de atualização de política chamando `PolicyUpdateListFactory.generatePolicyUpdateList()`. Da mesma forma, as políticas atualizadas podem ser adicionadas à lista usando `PolicyUpdateEntry`.
1. Se uma lista de atualização de política já existir, você poderá serializá-la para carregamento chamando `PolicyUpdateList.getBytes()`. Para carregar a lista, chame `PolicyUpdateListFactory.loadPolicyUpdateList()` e passar na lista serializada.
1. Verifique se a assinatura é válida e se a lista foi assinada pelo certificado de servidor de licenças correto chamando `PolicyUpdateList.verifySignature()`.
1. Para verificar se uma entrada foi revogada, transmita a ID da política `String` em `PolicyUpdateList.isRevoked()`. Como alternativa, a lista pode ser passada para `HandlerConfiguration` e será aplicado quando as licenças forem emitidas.

Para adicionar mais entradas a uma `PolicyUpdateList`, carregar uma lista de atualização de política existente. Criar um novo `PolicyUpdateListFactory` instância. Chame P `olicyUpdateListFactory.addEntries` para adicionar todas as entradas da lista antiga à nova lista. Chame `PolicyUpdateListFactory.addRevocationEntry` ou `addUpdatedEntry` para adicionar novas entradas de revogação ou atualização à PolicyUpdateList.

Para obter exemplos de código demonstrando como criar uma lista de atualização de política, carregar uma lista de atualização de política existente e verificar se uma política foi revogada, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` no diretório &quot;samples&quot; de Ferramentas de linha de comando de implementação de referência.
