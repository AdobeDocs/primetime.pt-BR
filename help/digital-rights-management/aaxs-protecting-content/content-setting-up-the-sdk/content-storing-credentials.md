---
seo-title: Armazenando credenciais
title: Armazenando credenciais
uuid: dbce523c-32d9-423f-bc95-39786f85fc29
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Armazenando credenciais{#storing-credentials}

O SDK oferece suporte a várias maneiras de armazenar credenciais (um certificado de chave pública e sua chave privada associada), inclusive em um HSM ou como um arquivo PKCS12. As credenciais são usadas quando a chave privada é necessária (por exemplo, para o empacotador assinar os metadados ou para o License Server descriptografar dados criptografados com o License Server ou a chave pública Transport). As chaves privadas devem ser acompanhadas de perto para garantir a segurança do seu conteúdo e do License Server. PKCS12 é um formato padrão para um arquivo que contém uma credencial criptografada usando uma senha. A extensão de arquivo .pfx geralmente é usada para arquivos desse formato.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>A Adobe recomenda usar um HSM para obter o máximo de segurança. Para obter mais informações, consulte as Diretrizes de implantação segura do Adobe Access.

>[!NOTE] {important=&quot;high&quot;}
>
>A partir do Java1.7, o Sun Java para Windows de 64 bits não oferece suporte às interfaces PKCS11 que o Adobe Access DRM requer para se comunicar com dispositivos HSM. Se você planeja usar um HSM, use uma versão de 32 bits do Java ou um JDK que suporte as interfaces completas do PKCS11.

Você pode manter uma chave privada em um HSM (Hardware Security Module, Módulo de segurança de hardware) e usar o SDK para transmitir a credencial obtida do HSM. Para usar uma credencial armazenada em um HSM, use um provedor JCE que possa se comunicar com um HSM para obter um identificador para a chave privada. Em seguida, passe o identificador da chave privada, o nome do provedor e o certificado que contém a chave pública para `ServerCredentialFactory.getServerCredential()`.

O provedor SunPKCS11 é um exemplo de um provedor JCE que pode ser usado para acessar uma chave privada em um HSM (consulte a documentação Sun Java para obter instruções sobre como usar esse provedor). Alguns HSMs também vêm com um Java SDK que inclui um provedor JCE.

PEM e DER são duas maneiras de codificar um certificado de chave pública. PEM é uma codificação base 64 e DER é uma codificação binária. Os arquivos de certificado normalmente usam a extensão .cer, .pem. ou .der. Os certificados são usados em locais onde apenas a chave pública é obrigatória. Se um componente exigir apenas a chave pública para operar, é melhor fornecer esse componente ao certificado em vez de uma credencial ou arquivo PKCS12.
