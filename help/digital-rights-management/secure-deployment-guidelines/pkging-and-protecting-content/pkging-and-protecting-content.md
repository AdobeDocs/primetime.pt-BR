---
description: As informações sobre o empacotamento e a proteção do conteúdo permitem que você proteja seu conteúdo.
title: Empacotamento e proteção de conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---


# Empacotamento e proteção de conteúdo {#packaging-protecting-content}

As informações sobre o empacotamento e a proteção do conteúdo permitem que você proteja seu conteúdo.

## Proteção do servidor {#securing-the-server}

Você precisa proteger fisicamente o computador em que o gerenciamento de políticas e o empacotamento de conteúdo ocorrem.

Para obter mais informações, consulte [Segurança física e acesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Se sua implementação de empacotamento de conteúdo exigir conectividade de rede, você deve endurecer seu sistema operacional e implementar uma solução de firewall apropriada. Para obter mais informações, consulte [Topologia de rede](../../secure-deployment-guidelines/overview/network-topology.md).

## Empacotar conteúdo com segurança {#securely-packaging-content}

O arquivo de configuração da ferramenta de linha de comando do Adobe Primetime DRM Media Packager requer uma credencial PKCS12 usada durante o empacotamento.

Nas ferramentas de implementação de referência do botão de controle, a senha do arquivo de credenciais PKCS12 é armazenada no arquivo `flashaccess.properties` em texto limpo. Por isso, tenha cuidado ao proteger o computador que hospeda esse arquivo e garantir que o computador esteja em um ambiente seguro. Para obter mais informações, consulte [Segurança física e acesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

O empacotador também usa os certificados de Transporte do License Server e do License Server e a integridade e confidencialidade dessas informações devem ser protegidas. Só as entidades autorizadas devem ser autorizadas a utilizar o embalador. Se suas chaves privadas estiverem comprometidas, informe o Adobe Systems Incorporated imediatamente para que o certificado possa ser revogado.

>[!NOTE]
>
>A API permite usar a mesma chave para vários conteúdos. Para garantir o mais alto nível de segurança, você só deve usar esse recurso para conteúdo FMS de taxa de bits múltipla. Não use a mesma chave para vários arquivos que representem conteúdo diferente.

A API de empacotamento de DRM do Primetime emite avisos sob determinadas condições. Revise esses avisos para determinar se os arquivos foram criptografados com êxito. As mensagens de aviso podem ser uma das seguintes:

* A política expirou e uma tag ou rastreamento não reconhecido não pode ser criptografada.
* Os fragmentos de filme não podem ser criptografados e as referências nesses fragmentos podem ser inválidas.
* Os metadados não podem ser criptografados.

Se o conteúdo for empacotado usando uma política com atributos incorretos, a política precisará ser atualizada. A política atualizada deve ser disponibilizada ao License Server por meio de uma lista de atualização de política ou outro mecanismo de delivery. Alguns atributos de política não podem ser alterados após a criação da política. Se esses atributos estiverem incorretos, puxe o conteúdo de volta dos sites de distribuição, revogue a política para que nenhuma licença futura possa ser concedida e criptografe o conteúdo novamente.

Quando o empacotamento é concluído, a chave de empacotamento é coletada com lixo e não é explicitamente destruída. Como resultado, a chave de empacotamento permanece presente na memória por algum tempo. Você deve proteger contra acesso não autorizado à máquina e garantir que não exponha arquivos, como despejos principais, que possam revelar essas informações.

## Armazenamento seguro de políticas {#securely-storing-policies}

O SDK de DRM da Adobe Primetime permite desenvolver aplicativos que podem ser usados em empacotamento de conteúdo e criação de políticas.

Ao criar esses aplicativos, você pode permitir que alguns usuários criem e modifiquem políticas e limitar outros usuários a aplicar somente as políticas existentes ao conteúdo. Você deve implementar os controles de acesso necessários e criar contas de usuário com privilégios diferentes para a criação de política e aplicação de política.

As políticas não são assinadas nem protegidas contra modificação até serem usadas em embalagens. Se estiver preocupado que os usuários da ferramenta de empacotamento possam modificar as políticas, assine as políticas para garantir que as políticas não possam ser modificadas.

Para obter mais informações sobre como criar aplicativos com o SDK, consulte as APIs de DRM do Primetime em [Referências da API do Primetime de API](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## Criptografia de chave assimétrica {#asymmetric-key-encryption}

A criptografia de chave assimétrica, também chamada de criptografia de chave pública, usa pares de chaves. Uma chave é para criptografia e a outra é para descriptografia.

A chave de descriptografia, ou *`private key`*, é mantida secreta; a chave de criptografia ou *`public key`* é disponibilizada para qualquer pessoa autorizada a criptografar conteúdo. Qualquer pessoa com acesso à chave pública pode criptografar o conteúdo. No entanto, somente alguém com acesso à chave privada pode descriptografar o conteúdo. A chave privada não pode ser reconstruída a partir da chave pública.

Ao empacotar conteúdo, a chave pública do License Server é usada para criptografar a chave de criptografia de conteúdo (CEK) nos metadados DRM. Você deve garantir que somente o License Server tenha acesso à chave privada do License Server. Se outra pessoa tiver a chave, ela poderá descriptografar e exibir o conteúdo.

>[!CAUTION]
>
>Certifique-se de obter o certificado do License Server que inclui a chave pública de uma fonte confiável. Dessa forma, você pode garantir que seja a chave do License Server e não uma chave pública desonesta. Se os atacantes substituíssem a chave pública pela chave do License Server, eles poderiam descriptografar seu conteúdo.

Para obter mais informações sobre como empacotar conteúdo, consulte [Usar o SDK de DRM do Adobe Primetime para proteger conteúdo](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).