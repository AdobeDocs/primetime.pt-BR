---
title: Criptografar conteúdo
description: Criptografar conteúdo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Criptografar conteúdo{#encrypting-content}

Você criptografa o conteúdo do vídeo com o objeto `MediaEncrypter`. Você pode criptografar arquivos de mídia que incluem apenas faixas de áudio. Também é possível aplicar apenas a criptografia parcial; por exemplo, para melhorar o desempenho ao criptografar o conteúdo H.264 para dispositivos de baixa definição.

Para criptografar arquivos de mídia usando a API do Java:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em *Setting up the development environment* no seu projeto.
1. Crie uma instância `ServerCredential` para carregar as credenciais necessárias para assinatura.
1. Crie uma instância `MediaEncrypter`. Use um `MediaEncryperFactory` se não souber qual tipo de arquivo possui.

1. Especifique as opções de criptografia usando um objeto `DRMParameters`.
1. Defina as opções de assinatura usando um objeto `SignatureParameters` e passe a instância `ServerCredential` para seu método `setServerCredentials`.

1. Defina a chave e as informações da licença usando um objeto `V2KeyParameters`. Defina as políticas de DRM usando o método `setPolicies`. Defina as informações necessárias para que o cliente entre em contato com o servidor de licenças, chamando os métodos `setLicenseServerUrl` e `setLicenseServerTransportCertificate`. Defina as opções de criptografia CEK usando o método `setKeyProtectionOptions` e suas propriedades personalizadas usando o método `setCustomProperties`. Finalmente, dependendo do tipo de criptografia usada, converta o objeto `DRMKeyParameters` no tipo apropriado ( `VideoDRMParameters`, `AudioDRMParameters`) e defina as opções de criptografia.

1. Criptografe o conteúdo transmitindo os arquivos de entrada e saída e as opções de criptografia para o método `MediaEncrypter.encryptContent`.

Para obter um código de amostra que mostra como criptografar o conteúdo, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` no diretório Ferramentas de linha de comando de implementação de referência [!DNL samples/] .
