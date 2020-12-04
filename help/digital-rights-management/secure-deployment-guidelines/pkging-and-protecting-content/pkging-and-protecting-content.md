---
description: As informações sobre o empacotamento e a proteção de conteúdo permitem que você proteja seu conteúdo.
seo-description: As informações sobre o empacotamento e a proteção de conteúdo permitem que você proteja seu conteúdo.
seo-title: Compactação e proteção de conteúdo
title: Compactação e proteção de conteúdo
uuid: 9bf89f86-082e-40f9-8deb-c9774a9d8e02
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---


# Empacotamento e proteção de conteúdo {#packaging-protecting-content}

As informações sobre o empacotamento e a proteção de conteúdo permitem que você proteja seu conteúdo.

## Protegendo o servidor {#securing-the-server}

É necessário proteger fisicamente o computador no qual o gerenciamento de políticas e o empacotamento de conteúdo ocorrem.

Para obter mais informações, consulte [Segurança física e acesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Se sua implementação de empacotamento de conteúdo exigir conectividade de rede, você deverá endurecer seu sistema operacional e implementar uma solução de firewall apropriada. Para obter mais informações, consulte [Topologia de rede](../../secure-deployment-guidelines/overview/network-topology.md).

## Empacotamento seguro de conteúdo {#securely-packaging-content}

O arquivo de configuração da ferramenta de linha de comando do Adobe Primetime DRM Media Packager requer uma credencial PKCS12 usada durante o empacotamento.

Nas ferramentas de script de comando de implementação de referência, a senha do arquivo de credenciais PKCS12 é armazenada no arquivo `flashaccess.properties` em texto limpo. Por esse motivo, tenha cuidado extra ao proteger o computador que hospeda esse arquivo e verifique se o computador está em um ambiente seguro. Para obter mais informações, consulte [Segurança física e acesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

O empacotador também usa os certificados de Transporte do License Server e do License Server e a integridade e confidencialidade dessas informações devem ser protegidas. Só as entidades autorizadas devem ser autorizadas a utilizar o embalador. Se suas chaves privadas estiverem comprometidas, informe imediatamente a Adobe Systems Incorporated para que o certificado possa ser revogado.

>[!NOTE]
>
>A API permite que você use a mesma chave para vários conteúdos. Para garantir o mais alto nível de segurança, você só deve usar esse recurso para conteúdo FMS de taxa de vários bits. Não use a mesma chave para vários arquivos que representem conteúdo diferente.

A Primetime DRM Packaging API emite avisos sob determinadas condições. Revise esses avisos para determinar se os arquivos foram criptografados com êxito. As mensagens de aviso podem ser uma das seguintes:

* A política expirou e uma tag ou rastreamento não reconhecido não pode ser criptografado.
* Os fragmentos de filme não podem ser criptografados e as referências nesses fragmentos podem ser inválidas.
* Metadados não podem ser criptografados.

Se o conteúdo for empacotado usando uma política com atributos incorretos, a política precisa ser atualizada. A política atualizada deve ser disponibilizada ao License Server por meio de uma lista de atualização de política ou de outro mecanismo de delivery. Alguns atributos de política não podem ser alterados depois que a política é criada. Se esses atributos estiverem incorretos, extraia o conteúdo dos sites de distribuição, revogue a política para que nenhuma licença futura possa ser concedida e criptografe o conteúdo novamente.

Quando o empacotamento é concluído, a chave de empacotamento é coletada pelo lixo e não é explicitamente destruída. Como resultado, a chave de empacotamento permanece presente na memória por algum tempo. Você deve proteger contra acesso não autorizado ao computador e garantir que não exponha arquivos, como os lixões principais, que possam revelar essas informações.

## Armazenando com segurança políticas {#securely-storing-policies}

O Adobe Primetime DRM SDK permite desenvolver aplicativos que podem ser usados em pacotes de conteúdo e criação de políticas.

Ao criar esses aplicativos, você pode permitir que alguns usuários criem e modifiquem políticas, além de limitar outros usuários a aplicar somente as políticas existentes ao conteúdo. Você deve implementar os controles de acesso necessários e criar contas de usuário com privilégios diferentes para a criação de políticas e aplicativos de políticas.

As políticas não são assinadas ou protegidas contra modificação até serem usadas em embalagens. Se você estiver preocupado que os usuários da ferramenta de empacotamento possam modificar políticas, assine as políticas para garantir que as políticas não possam ser modificadas.

Para obter mais informações sobre como criar aplicativos com o SDK, consulte as APIs DRM do Primetime em [Referências da API do Primetime da API](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## Criptografia de chave assimétrica {#asymmetric-key-encryption}

A criptografia de chave assimétrica, também chamada de criptografia de chave pública, usa pares de chaves. Uma chave é para criptografia, e a outra é para descriptografia.

A chave de decodificação, ou *`private key`*, é mantida secreta; a chave de criptografia, ou *`public key`*, é disponibilizada para qualquer pessoa autorizada a criptografar conteúdo. Qualquer pessoa com acesso à chave pública pode criptografar o conteúdo. No entanto, somente alguém com acesso à chave privada pode descriptografar o conteúdo. A chave privada não pode ser reconstruída a partir da chave pública.

Ao disponibilizar conteúdo, a chave pública do License Server é usada para criptografar a chave de criptografia de conteúdo (CEK) nos metadados do DRM. Você deve garantir que somente o License Server tenha acesso à chave privada do License Server. Se outra pessoa tiver a chave, ela poderá descriptografar e visualização o conteúdo.

>[!CAUTION]
>
>Certifique-se de obter o certificado do License Server que inclui a chave pública de uma fonte confiável. Dessa forma, você pode garantir que seja a chave do License Server e não uma chave pública desonesta. Se os atacantes substituírem a chave pública pela chave do License Server, eles poderão descriptografar seu conteúdo.

Para obter mais informações sobre como empacotar conteúdo, consulte [Usar o SDK do Adobe Primetime DRM para proteger conteúdo](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).