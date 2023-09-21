---
title: Armazenamento de credenciais
description: Armazenamento de credenciais
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Armazenamento de credenciais{#storing-credentials}

O SDK é compatível com várias maneiras de armazenar credenciais (um certificado de chave pública e sua chave privada associada), inclusive em um arquivo HSM ou PKCS12. As credenciais são usadas quando a chave privada é necessária (por exemplo, para que o empacotador assine os metadados ou para que o License Server descriptografe dados criptografados com o License Server ou a chave pública de transporte). As chaves privadas devem ser cuidadosamente protegidas para garantir a segurança do seu conteúdo e do Servidor de licenças. PKCS12 é um formato padrão para um arquivo que contém uma credencial criptografada usando uma senha. A extensão de arquivo .pfx é comumente usada para arquivos desse formato.

>[!NOTE]
>
>A Adobe recomenda o uso de um HSM para máxima segurança. Para obter mais informações, consulte as Diretrizes de implantação segura de acesso ao Adobe.

>[!NOTE]
>
>A partir do Java1.7, o Sun Java de 64 bits para Windows não suporta as interfaces PKCS11 que o DRM de acesso Adobe requer para se comunicar com dispositivos HSM. Se você planeja usar um HSM, use uma versão de 32 bits do Java ou use um JDK que suporte as interfaces PKCS11 completas.

Você pode manter uma chave privada em um HSM (Hardware Security Module, módulo de segurança de hardware) e usar o SDK para transmitir a credencial obtida do HSM. Para usar uma credencial armazenada em um HSM, use um provedor JCE que possa se comunicar com um HSM para obter um identificador para a chave privada. Em seguida, passe o identificador de chave privada, o nome do provedor e o certificado que contém a chave pública para `ServerCredentialFactory.getServerCredential()`.

O provedor SunPKCS11 é um exemplo de provedor JCE que pode ser usado para acessar uma chave privada em um HSM (consulte a documentação do Sun Java para obter instruções sobre o uso desse provedor). Alguns HSMs também vêm com um SDK Java que inclui um provedor JCE.

PEM e DER são duas maneiras de codificar um certificado de chave pública. PEM é uma codificação de base 64 e DER é uma codificação binária. Os arquivos de certificado normalmente usam a extensão .cer, .pem. ou .der. Os certificados são usados em locais onde somente a chave pública é necessária. Se um componente exigir apenas a chave pública para operar, é melhor fornecer esse componente com o certificado em vez de um arquivo de credencial ou PKCS12.
