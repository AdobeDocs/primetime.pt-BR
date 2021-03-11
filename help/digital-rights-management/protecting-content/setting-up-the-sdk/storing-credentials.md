---
title: Armazenando credenciais
description: Armazenando credenciais
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Armazenando credenciais{#storing-credentials}

O SDK de DRM do Primetime oferece suporte a diferentes maneiras de armazenar credenciais, incluindo o uso de um Módulo de segurança de hardware (HSM) ou como um arquivo PKCS12. O SDK usa uma credencial (certificado de chave pública e chave privada associada) quando a chave privada é necessária. Por exemplo, o empacotador usa uma credencial para assinar metadados; o License Server usa uma credencial para descriptografar dados que foram criptografados com a chave pública License Server ou Transport.

Você deve proteger de perto as chaves privadas para garantir a segurança do seu conteúdo e do License Server. PKCS12 é um formato de arquivo padrão para armazenar credenciais que foram criptografadas com uma senha. (Você também pode criptografar e assinar o próprio arquivo PKCS12.) A extensão de arquivo [!DNL .pfx] é comumente usada para arquivos que oferecem suporte a esse formato.

>[!NOTE]
>
>O Adobe recomenda usar um HSM para obter o máximo de segurança.
>
>Consulte o guia *Diretrizes de implantação segura do Adobe Primetime DRM*.

>[!NOTE]
>
>Desde o Java 1.7, o Sun Java para Windows de 64 bits não é mais compatível com as interfaces PKCS11 que o Primetime DRM requer para comunicação com dispositivos HSM. Se você planeja usar um HSM, é necessário usar uma versão de 32 bits do Java ou usar um JDK que ofereça suporte a todas as interfaces PKCS11.

Você pode manter uma chave privada em um HSM e usar o SDK de DRM do Primetime para transmitir a credencial obtida do HSM. Se quiser usar uma credencial armazenada em um HSM, é necessário usar um provedor JCE que possa se comunicar com um HSM para obter um identificador para a chave privada. Em seguida, é necessário transmitir o identificador da chave privada, o nome do provedor e o certificado que inclui a chave pública para `ServerCredentialFactory.getServerCredential()`.

O provedor SunPKCS11 representa um exemplo de um provedor JCE que você pode usar para acessar uma chave privada em um HSM. Alguns HSMs também estão incluídos com um SDK Java fornecido com um provedor JCE.

Consulte a documentação do Sun Java para obter instruções sobre como usar esse provedor.

PEM e DER são maneiras de codificar um certificado de chave pública. PEM é uma codificação base 64 e DER é uma codificação binária. Os arquivos de certificado normalmente usam a extensão [!DNL .cer], [!DNL .pem] ou [!DNL .der]. Os certificados são usados quando somente uma chave pública é necessária. Se um componente exigir apenas a chave pública para funcionar, é recomendável fornecer esse componente com o certificado em vez de uma credencial ou arquivo PKCS12.
