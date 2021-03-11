---
title: Armazenando credenciais
description: Armazenando credenciais
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Armazenando credenciais{#storing-credentials}

O SDK oferece suporte a várias maneiras de armazenar credenciais (um certificado de chave pública e sua chave privada associada), incluindo em um HSM ou como um arquivo PKCS12. As credenciais são usadas quando a chave privada é necessária (por exemplo, para o empacotador assinar os metadados ou para o License Server descriptografar dados criptografados com o License Server ou a chave pública Transport). As chaves privadas devem estar bem protegidas para garantir a segurança do seu conteúdo e do License Server. PKCS12 é um formato padrão para um arquivo que contém uma credencial criptografada por meio de uma senha. A extensão de arquivo .pfx geralmente é usada para arquivos desse formato.

>[!NOTE]
>
>A Adobe recomenda usar um HSM para obter segurança máxima. Para obter mais informações, consulte as Diretrizes de implantação segura do Adobe Access .

>[!NOTE]
>
>A partir do Java1.7, o Sun Java para Windows de 64 bits não é compatível com as interfaces PKCS11 que o DRM do Adobe Access requer para se comunicar com dispositivos HSM. Se você planeja usar um HSM, use uma versão de 32 bits do Java ou um JDK que seja compatível com todas as interfaces PKCS11.

Você pode manter uma chave privada em um HSM (Hardware Security Module, Módulo de segurança de hardware) e usar o SDK para transmitir a credencial obtida do HSM. Para usar uma credencial armazenada em um HSM, use um provedor JCE que possa se comunicar com um HSM para obter um identificador para a chave privada. Em seguida, passe o identificador da chave privada, o nome do provedor e o certificado que contém a chave pública para `ServerCredentialFactory.getServerCredential()`.

O provedor SunPKCS11 é um exemplo de um provedor JCE que pode ser usado para acessar uma chave privada em um HSM (consulte a documentação do Sun Java para obter instruções sobre como usar esse provedor). Alguns HSMs também vêm com um SDK Java que inclui um provedor JCE.

PEM e DER são duas maneiras de codificar um certificado de chave pública. PEM é uma codificação base 64 e DER é uma codificação binária. Os arquivos de certificado normalmente usam a extensão .cer, .pem. ou .der. Os certificados são usados em locais onde somente a chave pública é obrigatória. Se um componente exigir apenas a chave pública para funcionar, é melhor fornecer o certificado a esse componente em vez de uma credencial ou arquivo PKCS12.
