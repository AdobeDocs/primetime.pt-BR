---
seo-title: Criptografar conteúdo
title: Criptografar conteúdo
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Criptografar conteúdo{#encrypting-content}

Você criptografa o conteúdo do vídeo com o objeto `MediaEncrypter`. É possível criptografar arquivos de mídia que incluam somente faixas de áudio. Você também pode aplicar apenas criptografia parcial; por exemplo, para melhorar o desempenho ao criptografar o conteúdo H.264 para dispositivos de baixa definição.

Para criptografar arquivos de mídia usando a API Java:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em *Configurar o ambiente de desenvolvimento* no seu projeto.
1. Crie uma instância `ServerCredential` para carregar as credenciais necessárias para assinatura.
1. Crie uma instância `MediaEncrypter`. Use `MediaEncryperFactory` se você não souber que tipo de arquivo possui.

1. Especifique as opções de criptografia usando um objeto `DRMParameters`.
1. Defina as opções de assinatura usando um objeto `SignatureParameters` e passe a instância `ServerCredential` para seu método `setServerCredentials`.

1. Defina as informações de chave e licença usando um objeto `V2KeyParameters`. Defina as políticas de DRM usando o método `setPolicies`. Defina as informações necessárias para que o cliente entre em contato com o servidor de licenças, chamando os métodos `setLicenseServerUrl` e `setLicenseServerTransportCertificate`. Defina as opções de criptografia CEK usando o método `setKeyProtectionOptions` e suas propriedades personalizadas usando o método `setCustomProperties`. Finalmente, dependendo do tipo de criptografia usada, converta o objeto `DRMKeyParameters` no tipo apropriado ( `VideoDRMParameters`, `AudioDRMParameters`) e defina as opções de criptografia.

1. Criptografe o conteúdo transmitindo os arquivos de entrada e saída e as opções de criptografia para o método `MediaEncrypter.encryptContent`.

Para obter um exemplo de código que mostra como criptografar conteúdo, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` no diretório Ferramentas de Linha de Comando de Implementação de Referência [!DNL samples/].
