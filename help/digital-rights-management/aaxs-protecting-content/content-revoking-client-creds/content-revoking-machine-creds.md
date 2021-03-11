---
title: Revogando credenciais da máquina
description: Revogando credenciais da máquina
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Revogando credenciais da máquina{#revoking-machine-credentials}

O Adobe mantém uma CRL para revogar credenciais de máquina conhecidas como comprometidas. Esta CRL é automaticamente aplicada pelo SDK. Se houver máquinas adicionais para as quais você não deseja que o servidor de licenças emita licenças, você pode criar uma lista de revogação de máquina e adicionar o nome do emissor e o número de série dos tokens de máquina que deseja excluir (use `MachineToken.getMachineTokenId()` para recuperar o nome do emissor e o número de série do certificado da máquina).

As credenciais da máquina de revogação envolvem o uso de um objeto `RevocationListFactory`. Para criar uma lista de revogação, carregar uma lista de revogação existente e verificar se um token de máquina foi revogado usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em [Setting up the development environment](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) no seu projeto.
1. Crie uma instância `ServerCredentialFactory` para carregar as credenciais necessárias para assinatura. A credencial do servidor de licenças é usada para assinar a lista de revogação.
1. Crie uma instância `RevocationListFactory`.
1. Especifique o emissor e o número de série do token de máquina a ser revogado usando um objeto `IssuerAndSerialNumber`. Todas as solicitações de Adobe Access contêm um token de máquina.
1. Crie um objeto `RevocationList` usando o objeto `IssuerAndSerialNumber` que acabou de criar e adicione-o à lista de revogação ao passá-lo para `RevocationListFactory.addRevocationEntry()`. Gere a nova lista de revogação chamando `RevocationListFactory.generateRevocationList()`.
1. Para salvar a lista de revogação, você pode serializá-la chamando `RevocationList.getBytes()`. Para carregar a lista, chame `RevocationListFactory.loadRevocationList()` e passe na lista serializada.
1. Verifique se a assinatura é válida e se a lista foi assinada pelo servidor de licenças correto ao chamar `RevocationList.verifySignature()`.
1. Para verificar se uma entrada foi revogada, passe o objeto `IssuerAndSerialNumber` para `RevocationList.isRevoked()`. A lista de revogação também pode ser passada para `HandlerConfiguration` para que o SDK imponha a lista de revogação para todas as solicitações de autenticação e licença.

Para adicionar mais entradas a um `RevocationList` existente, carregue uma lista de revogação existente. Crie uma nova instância `RevocationListFactory` e certifique-se de incrementar o número do CRL. Chame `RevocationListFactioryEntries.addRevocationEntries` para adicionar todas as entradas da lista antiga à nova lista. Chame `RevocationListFactory.addRevocationEntry` para adicionar novas entradas de revogação à Lista de Revogação.

Para obter um código de amostra que demonstre como criar uma lista de revogação, carregar uma lista de revogação existente e verificar se um token de máquina foi revogado, consulte `com.adobe.flashaccess.samples.revocation.CreateRevocationList` no diretório &quot;samples&quot; de Ferramentas de Linha de Comando de Implementação de Referência.
