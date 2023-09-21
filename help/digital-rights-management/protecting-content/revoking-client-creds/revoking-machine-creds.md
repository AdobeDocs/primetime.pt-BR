---
title: Revogando credenciais da máquina
description: Revogando credenciais da máquina
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# Revogando credenciais da máquina {#revoking-machine-credentials}

O Adobe mantém uma CRL para revogar credenciais de máquina que são conhecidas por estarem comprometidas. Essa CRL é aplicada automaticamente pelo SDK. Se houver computadores adicionais para os quais você não deseja que o servidor de licenças emita licenças, crie uma lista de revogação de computador e adicione o nome do emissor e o número de série dos tokens de computador que deseja excluir (use `MachineToken.getMachineTokenId()` para recuperar o nome do emissor e o número de série do certificado do computador).

A revogação de credenciais de máquina envolve o uso de um `RevocationListFactory` objeto. Para criar uma lista de revogação, carregar uma lista de revogação existente e verificar se um token de máquina foi revogado usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em [Configuração do ambiente de desenvolvimento](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) no seu projeto.
1. Criar um `ServerCredentialFactory` para carregar as credenciais necessárias para assinatura. A credencial do servidor de licenças é usada para assinar a lista de revogação.
1. Criar um `RevocationListFactory` instância.
1. Especifique o emissor e o número de série do token do computador a ser revogado usando um `IssuerAndSerialNumber` objeto. Todas as solicitações DRM do Adobe Primetime contêm um token de computador.
1. Criar um `RevocationList` objeto usando o `IssuerAndSerialNumber` objeto que você acabou de criar, e adicione-o à lista de revogação passando-o para `RevocationListFactory.addRevocationEntry()`. Gerar a nova lista de revogação chamando `RevocationListFactory.generateRevocationList()`.

1. Para salvar a lista de revogação, você pode serializá-la chamando `RevocationList.getBytes()`. Para carregar a lista, chame `RevocationListFactory.loadRevocationList()` e passar na lista serializada.

1. Verifique se a assinatura é válida e se a lista foi assinada pelo servidor de licenças correto chamando `RevocationList.verifySignature()`.
1. Para verificar se uma entrada foi revogada, transmita a `IssuerAndSerialNumber` objeto em `RevocationList.isRevoked()`. A lista de revogação pode também ser `HandlerConfiguration` para que o SDK imponha a lista de revogação para todas as solicitações de autenticação e licença.

Para adicionar mais entradas a uma `RevocationList`, carregar uma lista de revogação existente. Criar um novo `RevocationListFactory` e certifique-se de incrementar o número da CRL. Chame `RevocationListFactioryEntries.addRevocationEntries` para adicionar todas as entradas da lista antiga à nova lista. Chame `RevocationListFactory.addRevocationEntry` para adicionar novas entradas de revogação à RevocationList.

Para obter o código de amostra que demonstra como criar uma lista de revogação, carregar uma lista de revogação existente e verificar se um token de computador foi revogado, consulte `com.adobe.flashaccess.samples.revocation.CreateRevocationList` nas Ferramentas de linha de comando da Implementação de referência [!DNL samples] diretório.
