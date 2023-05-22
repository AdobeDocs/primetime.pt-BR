---
title: Criptografar conteúdo
description: Criptografar conteúdo
copied-description: true
exl-id: c6b5d8c7-eda4-40c0-a609-0ebfeba90c04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Criptografar conteúdo{#encrypting-content}

Você criptografa o conteúdo de vídeo com o `MediaEncrypter` objeto. Você pode criptografar arquivos de mídia que incluem apenas faixas de áudio. Também é possível aplicar somente a criptografia parcial; por exemplo, para melhorar o desempenho ao criptografar o conteúdo H.264 para dispositivos mais simples.

Para criptografar arquivos de mídia usando a API Java:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em *Configuração do ambiente de desenvolvimento* no seu projeto.
1. Criar um `ServerCredential` para carregar as credenciais necessárias para assinatura.
1. Criar um `MediaEncrypter` instância. Use um `MediaEncryperFactory` caso não saiba o tipo de arquivo que possui.

1. Especifique as opções de criptografia usando um `DRMParameters` objeto.
1. Defina as opções de assinatura usando uma `SignatureParameters` e transmita o `ServerCredential` à sua `setServerCredentials` método.

1. Defina a chave e as informações de licença usando um `V2KeyParameters` objeto. Defina as políticas de DRM usando o `setPolicies` método. Defina as informações necessárias para o cliente entrar em contato com o servidor de licenças, chamando o `setLicenseServerUrl` e `setLicenseServerTransportCertificate` métodos. Defina as opções de criptografia do CEK usando o `setKeyProtectionOptions` e suas propriedades personalizadas usando o `setCustomProperties` método. Finalmente, dependendo do tipo de criptografia usada, converta o `DRMKeyParameters` ao tipo apropriado ( `VideoDRMParameters`, `AudioDRMParameters`) e defina as opções de criptografia.

1. Criptografe o conteúdo passando os arquivos de entrada e saída e as opções de criptografia para o `MediaEncrypter.encryptContent` método.

Para obter o código de exemplo que mostra como criptografar o conteúdo, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` nas Ferramentas de linha de comando da Implementação de referência [!DNL samples/] diretório.
