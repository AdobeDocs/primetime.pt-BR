---
title: Criptografar conteúdo
description: Criptografar conteúdo
copied-description: true
exl-id: 84a490ae-af0c-43c5-a849-ed832e83a28d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Criptografar conteúdo{#encrypting-content}

A criptografia de conteúdo FLV e F4V envolve o uso de um `MediaEncrypter` objeto. Também é possível empacotar arquivos FLV e F4V que contenham apenas faixas de áudio. Ao criptografar o conteúdo H.264 para dispositivos low-end, pode ser prático aplicar somente criptografia parcial para melhorar o desempenho. Nesses casos, um arquivo F4V pode ser parcialmente criptografado usando o `F4VDRMParameters.setVideoEncryptionLevel`método.

Para criptografar um arquivo FLV ou F4V usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em Configuração do ambiente de desenvolvimento no seu projeto.
1. Criar um `ServerCredential` para carregar as credenciais necessárias para assinatura.
1. Criar um `MediaEncrypter` instância. Use um `MediaEncryperFactory` caso não saiba o tipo de arquivo que possui. Caso contrário, você poderá criar um `FLVEncrypter` ou `F4VEncrypter` diretamente.
1. Especifique as opções de criptografia usando um `DRMParameters` objeto.
1. Defina as opções de assinatura usando uma `SignatureParameters` e transmita o `ServerCredential` à sua `setServerCredentials` método.
1. Defina a chave e as informações de licença usando um `V2KeyParameters` objeto. Defina as políticas usando o `setPolicies` método. Defina as informações necessárias para o cliente entrar em contato com o servidor de licenças, chamando o `setLicenseServerUrl` e `setLicenseServerTransportCertificate` métodos. Defina as opções de criptografia do CEK usando o `setKeyProtectionOptions` e suas propriedades personalizadas usando o `setCustomProperties` método. Finalmente, dependendo do tipo de criptografia usada, converta o `DRMKeyParameters` objeto para um de `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`ou `F4VDRMParameters`e defina as opções de criptografia.
1. Criptografe o conteúdo passando os arquivos de entrada e saída e as opções de criptografia para o `MediaEncrypter.encryptContent` método.

Para obter exemplos de código demonstrando como criptografar o conteúdo, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` no diretório &quot;samples&quot; de Ferramentas de linha de comando de implementação de referência.
