---
title: Criptografar conteúdo
description: Criptografar conteúdo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Criptografar conteúdo{#encrypting-content}

A criptografia de conteúdo FLV e F4V envolve o uso de um objeto `MediaEncrypter`. Você também pode empacotar arquivos FLV e F4V que contêm apenas faixas de áudio. Ao criptografar conteúdo H.264 para dispositivos de baixa definição, pode ser prático aplicar apenas criptografia parcial para melhorar o desempenho. Nesses casos, um arquivo F4V pode ser parcialmente criptografado usando o método `F4VDRMParameters.setVideoEncryptionLevel`.

Para criptografar um arquivo FLV ou F4V usando a API do Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em Configuração do ambiente de desenvolvimento em seu projeto.
1. Crie uma instância `ServerCredential` para carregar as credenciais necessárias para assinatura.
1. Crie uma instância `MediaEncrypter`. Use um `MediaEncryperFactory` se não souber qual tipo de arquivo possui. Caso contrário, você poderá criar um `FLVEncrypter` ou `F4VEncrypter` diretamente.
1. Especifique as opções de criptografia usando um objeto `DRMParameters`.
1. Defina as opções de assinatura usando um objeto `SignatureParameters` e passe a instância `ServerCredential` para seu método `setServerCredentials`.
1. Defina a chave e as informações da licença usando um objeto `V2KeyParameters`. Defina as políticas usando o método `setPolicies`. Defina as informações necessárias para que o cliente entre em contato com o servidor de licenças, chamando os métodos `setLicenseServerUrl` e `setLicenseServerTransportCertificate`. Defina as opções de criptografia CEK usando o método `setKeyProtectionOptions` e suas propriedades personalizadas usando o método `setCustomProperties`. Finalmente, dependendo do tipo de criptografia usada, converta o objeto `DRMKeyParameters` em um dos `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters` ou `F4VDRMParameters` e defina as opções de criptografia.
1. Criptografe o conteúdo transmitindo os arquivos de entrada e saída e as opções de criptografia para o método `MediaEncrypter.encryptContent`.

Para obter um código de amostra que demonstra como criptografar o conteúdo, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` no diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência.
