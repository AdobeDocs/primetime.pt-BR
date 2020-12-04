---
seo-title: Armazenando credenciais
title: Armazenando credenciais
uuid: a9e9db72-c921-4c28-ad1d-3fd3c2283f14
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Armazenando credenciais{#storing-credentials}

O SDK do DRM Primetime oferece suporte a diferentes maneiras de armazenar credenciais, incluindo o uso de um HSM (Hardware Security Module) ou como um arquivo PKCS12. O SDK usa uma credencial (certificado de chave pública e chave privada associada) quando a chave privada é obrigatória. Por exemplo, o empacotador usa uma credencial para assinar metadados; o License Server usa uma credencial para descriptografar dados que foram criptografados com o License Server ou a chave pública Transport.

Você deve proteger com atenção as chaves privadas para garantir a segurança do seu conteúdo e do License Server. PKCS12 é um formato de arquivo padrão para armazenar credenciais que foram criptografadas com uma senha. (Você também pode criptografar e assinar o próprio arquivo PKCS12.) A extensão de arquivo [!DNL .pfx] é comumente usada para arquivos compatíveis com esse formato.

>[!NOTE]
>
>A Adobe recomenda usar um HSM para obter o máximo de segurança.
>
>Consulte o guia *Diretrizes de Implantação Segura do Adobe Primetime DRM*.

>[!NOTE]
>
>A partir do Java 1.7, o Sun Java para Windows de 64 bits não oferece mais suporte às interfaces PKCS11 que o Primetime DRM exige para comunicação com dispositivos HSM. Se você planeja usar um HSM, é necessário usar uma versão de 32 bits do Java ou usar um JDK que suporte as interfaces completas do PKCS11.

Você pode manter uma chave privada em um HSM e usar o SDK DRM Primetime para passar a credencial obtida do HSM. Se você quiser usar uma credencial armazenada em um HSM, é necessário usar um provedor JCE que possa se comunicar com um HSM para obter um identificador para a chave privada. Em seguida, você precisa passar o identificador de chave privada, o nome do provedor e o certificado que inclui a chave pública para `ServerCredentialFactory.getServerCredential()`.

O provedor SunPKCS11 representa um exemplo de um provedor JCE que você pode usar para acessar uma chave privada em um HSM. Alguns HSMs também estão incluídos com um Java SDK fornecido com um provedor JCE.

Consulte a documentação Sun Java para obter instruções sobre como usar esse provedor.

PEM e DER são formas de codificar um certificado de chave pública. PEM é uma codificação base 64 e DER é uma codificação binária. Os arquivos de certificado normalmente usam a extensão [!DNL .cer], [!DNL .pem] ou [!DNL .der]. Certificados são usados onde apenas uma chave pública é necessária. Se um componente exigir apenas a chave pública para operar, é recomendável que você forneça esse componente ao certificado em vez de uma credencial ou um arquivo PKCS12.
