---
seo-title: Criptografar conteúdo
title: Criptografar conteúdo
uuid: ea71154e-557b-447e-bc14-208232f00be1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Criptografar conteúdo{#encrypting-content}

A criptografia de conteúdo FLV e F4V envolve o uso de um `MediaEncrypter` objeto. Você também pode empacotar arquivos FLV e F4V que contêm somente faixas de áudio. Ao criptografar o conteúdo H.264 para dispositivos de baixa definição, pode ser prático aplicar apenas criptografia parcial para melhorar o desempenho. Nesses casos, um arquivo F4V pode ser parcialmente criptografado usando o `F4VDRMParameters.setVideoEncryptionLevel`método.

Para criptografar um arquivo FLV ou F4V usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em Configurando o ambiente de desenvolvimento dentro do projeto.
1. Crie uma `ServerCredential` instância para carregar as credenciais necessárias para assinatura.
1. Crie uma `MediaEncrypter` instância. Use um arquivo `MediaEncryperFactory` se você não souber que tipo de arquivo possui. Caso contrário, você poderá criar um `FLVEncrypter` ou `F4VEncrypter` diretamente.
1. Especifique as opções de criptografia usando um `DRMParameters` objeto.
1. Defina as opções de assinatura usando um `SignatureParameters` objeto e passe a `ServerCredential` instância para seu `setServerCredentials` método.
1. Defina as informações de chave e licença usando um `V2KeyParameters` objeto. Defina as políticas usando o `setPolicies` método. Defina as informações necessárias para que o cliente entre em contato com o servidor de licenças, chamando os métodos `setLicenseServerUrl` e `setLicenseServerTransportCertificate` . Defina as opções de criptografia CEK usando o `setKeyProtectionOptions` método e suas propriedades personalizadas usando o `setCustomProperties` método. Por fim, dependendo do tipo de criptografia usada, converta o `DRMKeyParameters` objeto em uma das opções de criptografia `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`ou `F4VDRMParameters`.
1. Criptografe o conteúdo transmitindo os arquivos de entrada e saída e as opções de criptografia para o `MediaEncrypter.encryptContent` método.

Para obter um exemplo de código que demonstra como criptografar o conteúdo, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` o diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência.
