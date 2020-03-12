---
seo-title: Criptografar conteúdo
title: Criptografar conteúdo
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Criptografar conteúdo{#encrypting-content}

Você criptografa o conteúdo do vídeo com o `MediaEncrypter` objeto. É possível criptografar arquivos de mídia que incluam somente faixas de áudio. Você também pode aplicar apenas criptografia parcial; por exemplo, para melhorar o desempenho ao criptografar o conteúdo H.264 para dispositivos de baixa definição.

Para criptografar arquivos de mídia usando a API Java:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em *Configurar o ambiente* de desenvolvimento dentro do projeto.
1. Crie uma `ServerCredential` instância para carregar as credenciais necessárias para assinatura.
1. Crie uma `MediaEncrypter` instância. Use um arquivo `MediaEncryperFactory` se você não souber que tipo de arquivo possui.

1. Especifique as opções de criptografia usando um `DRMParameters` objeto.
1. Defina as opções de assinatura usando um `SignatureParameters` objeto e passe a `ServerCredential` instância para seu `setServerCredentials` método.

1. Defina as informações de chave e licença usando um `V2KeyParameters` objeto. Defina as políticas de DRM usando o `setPolicies` método. Defina as informações necessárias para que o cliente entre em contato com o servidor de licenças, chamando os métodos `setLicenseServerUrl` e `setLicenseServerTransportCertificate` . Defina as opções de criptografia CEK usando o `setKeyProtectionOptions` método e suas propriedades personalizadas usando o `setCustomProperties` método. Por fim, dependendo do tipo de criptografia usada, converta o `DRMKeyParameters` objeto no tipo apropriado ( `VideoDRMParameters`, `AudioDRMParameters`) e defina as opções de criptografia.

1. Criptografe o conteúdo transmitindo os arquivos de entrada e saída e as opções de criptografia para o `MediaEncrypter.encryptContent` método.

Para obter um exemplo de código que mostra como criptografar o conteúdo, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` o diretório Ferramentas de Linha de Comando de Implementação de Referência [!DNL samples/] .
