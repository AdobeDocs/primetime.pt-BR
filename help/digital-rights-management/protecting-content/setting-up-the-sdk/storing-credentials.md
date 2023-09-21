---
title: Armazenamento de credenciais
description: Armazenamento de credenciais
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Armazenamento de credenciais{#storing-credentials}

O SDK do DRM do Primetime oferece suporte a diferentes maneiras de armazenar credenciais, incluindo o uso de um Módulo de segurança de hardware (HSM) ou como um arquivo PKCS12. O SDK usa uma credencial (certificado de chave pública e chave privada associada) quando a chave privada é necessária. Por exemplo, o empacotador usa uma credencial para assinar metadados; o License Server usa uma credencial para descriptografar dados que foram criptografados com o License Server ou a chave pública de Transporte.

Você deve proteger cuidadosamente as chaves privadas para garantir a segurança do seu conteúdo e do Servidor de licenças. PKCS12 é um formato de arquivo padrão para armazenar credenciais que foram criptografadas com uma senha. (Você também pode criptografar e assinar o próprio arquivo PKCS12.) A extensão do arquivo [!DNL .pfx] O geralmente é usado para arquivos que oferecem suporte a esse formato.

>[!NOTE]
>
>A Adobe recomenda o uso de um HSM para segurança máxima.
>
>Consulte a *Diretrizes de implantação segura do Adobe Primetime DRM* guia.

>[!NOTE]
>
>A partir do Java 1.7, o Sun Java de 64 bits para Windows não oferecerá mais suporte às interfaces PKCS11 exigidas pelo Primetime DRM para comunicação com dispositivos HSM. Se você planeja usar um HSM, precisa usar uma versão de 32 bits do Java, ou usar um JDK que suporte as interfaces PKCS11 completas.

Você pode manter uma chave privada em um HSM e usar o SDK DRM do Primetime para transmitir a credencial obtida do HSM. Se você quiser usar uma credencial armazenada em um HSM, será necessário usar um provedor JCE que possa se comunicar com um HSM para obter um identificador para a chave privada. Em seguida, é necessário passar o identificador da chave privada, o nome do provedor e o certificado que inclui a chave pública para `ServerCredentialFactory.getServerCredential()`.

O provedor SunPKCS11 representa um exemplo de provedor JCE que você pode usar para acessar uma chave privada em um HSM. Alguns HSMs também estão incluídos com um SDK Java fornecido com um provedor JCE.

Consulte a documentação do Sun Java para obter instruções sobre como usar este provedor.

PEM e DER são maneiras de codificar um certificado de chave pública. PEM é uma codificação de base 64 e DER é uma codificação binária. Os arquivos de certificado normalmente usam a extensão [!DNL .cer], [!DNL .pem]ou [!DNL .der]. Os certificados são usados quando é necessária apenas uma chave pública. Se um componente exigir apenas a chave pública para operar, é recomendável fornecer esse componente com o certificado em vez de um arquivo de credencial ou PKCS12.
