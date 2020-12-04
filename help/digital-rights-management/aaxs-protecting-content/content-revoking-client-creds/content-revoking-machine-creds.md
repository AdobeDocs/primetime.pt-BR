---
seo-title: Revogando credenciais da máquina
title: Revogando credenciais da máquina
uuid: 16119ff9-8147-4fe0-9744-a705d94a9400
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Revogando credenciais do computador{#revoking-machine-credentials}

O Adobe mantém uma CRL por revogar credenciais da máquina que se sabe estarem comprometidas. Esta CRL é automaticamente imposta pelo SDK. Se houver máquinas adicionais para as quais você não deseja que o servidor de licenças emita licenças, você pode criar uma lista de revogação de máquina e adicionar o nome do emissor e o número de série dos tokens de máquina que deseja excluir (use `MachineToken.getMachineTokenId()` para recuperar o nome do emissor e o número de série do certificado de máquina).

Revogar credenciais do computador envolve o uso de um objeto `RevocationListFactory`. Para criar uma lista de revogação, carregar uma lista de revogação existente e verificar se um token de máquina foi revogado usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em [Configurar o ambiente de desenvolvimento](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) no seu projeto.
1. Crie uma instância `ServerCredentialFactory` para carregar as credenciais necessárias para assinatura. A credencial do servidor de licenças é usada para assinar a lista de revogação.
1. Crie uma instância `RevocationListFactory`.
1. Especifique o emissor e o número de série do token de máquina a ser revogado usando um objeto `IssuerAndSerialNumber`. Todas as solicitações de acesso a Adobe contêm um token de máquina.
1. Crie um objeto `RevocationList` usando o objeto `IssuerAndSerialNumber` que você acabou de criar e adicione-o à lista de revogação transmitindo-o para `RevocationListFactory.addRevocationEntry()`. Gere a nova lista de revogação chamando `RevocationListFactory.generateRevocationList()`.
1. Para salvar a lista de revogação, você pode serializá-la chamando `RevocationList.getBytes()`. Para carregar a lista, chame `RevocationListFactory.loadRevocationList()` e passe na lista serializada.
1. Verifique se a assinatura é válida e se a lista foi assinada pelo servidor de licenças correto, ligando para `RevocationList.verifySignature()`.
1. Para verificar se uma entrada foi revogada, passe o objeto `IssuerAndSerialNumber` para `RevocationList.isRevoked()`. A lista de revogação também pode ser passada para `HandlerConfiguration` para que o SDK aplique a lista de revogação para todas as solicitações de autenticação e licença.

Para adicionar entradas adicionais a um `RevocationList` existente, carregue uma lista de revogação existente. Crie uma nova instância `RevocationListFactory` e certifique-se de incrementar o número CRL. Chame `RevocationListFactioryEntries.addRevocationEntries` para adicionar todas as entradas da lista antiga à nova lista. Chame `RevocationListFactory.addRevocationEntry` para adicionar novas entradas de revogação à RevocationList.

Para obter um exemplo de código que demonstra como criar uma lista de revogação, carregar uma lista de revogação existente e verificar se um token de máquina foi revogado, consulte `com.adobe.flashaccess.samples.revocation.CreateRevocationList` no diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência.
