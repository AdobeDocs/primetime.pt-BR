---
description: As informações sobre empacotamento e proteção de conteúdo permitem que você proteja seu conteúdo.
title: Empacotamento e proteção de componentes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Empacotamento e proteção de conteúdo {#packaging-protecting-content}

As informações sobre empacotamento e proteção de conteúdo permitem que você proteja seu conteúdo.

## Proteção do servidor {#securing-the-server}

Você precisa proteger fisicamente o computador no qual ocorre o gerenciamento de políticas e o empacotamento de conteúdo.

Para obter mais informações, consulte [Segurança física e acesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Se a implementação do pacote de conteúdo exigir conectividade de rede, você deverá fortalecer o sistema operacional e implementar uma solução de firewall apropriada. Para obter mais informações, consulte [Topologia de rede](../../secure-deployment-guidelines/overview/network-topology.md).

## Empacotando conteúdo com segurança {#securely-packaging-content}

O arquivo de configuração da ferramenta de linha de comando do Adobe Primetime DRM Media Packager requer uma credencial PKCS12 usada durante o empacotamento.

Nas ferramentas de linha de comando da Implementação de referência, a senha do arquivo de credenciais PKCS12 é armazenada no `flashaccess.properties` arquivo em texto não criptografado. Por esse motivo, tenha mais cuidado ao proteger o computador que hospeda esse arquivo e verifique se o computador está em um ambiente seguro. Para obter mais informações, consulte [Segurança física e acesso](../../secure-deployment-guidelines/physical-sec-and-access.md).

O empacotador também usa os certificados de transporte do License Server e do License Server, e a integridade e a confidencialidade dessas informações devem ser protegidas. Apenas as entidades autorizadas devem ser autorizadas a utilizar o acondicionador. Se suas chaves privadas estiverem comprometidas, informe o Adobe Systems Incorporated imediatamente para que o certificado possa ser revogado.

>[!NOTE]
>
>A API permite usar a mesma chave para vários conteúdos. Para garantir o mais alto nível de segurança, você só deve usar esse recurso para conteúdo FMS com taxa de vários bits. Não use a mesma chave para vários arquivos que representam conteúdo diferente.

A API de empacotamento DRM do Primetime emite avisos sob determinadas condições. Examine esses avisos para determinar se os arquivos foram criptografados com êxito. As mensagens de aviso podem ser uma das seguintes:

* A política expirou e uma tag ou faixa não reconhecida não pode ser criptografada.
* Os fragmentos de filme não podem ser criptografados e as referências dentro desses fragmentos podem ser inválidas.
* Não é possível criptografar metadados.

Se o conteúdo for empacotado usando uma política com atributos incorretos, a política precisará ser atualizada. A política atualizada deve ser disponibilizada ao License Server por meio de uma lista de atualização de política ou outro mecanismo de entrega. Alguns atributos de política não podem ser alterados após a criação da política. Se esses atributos estiverem incorretos, retire o conteúdo dos sites de distribuição, revogue a política para que nenhuma licença futura possa ser concedida e criptografe o conteúdo novamente.

Quando o empacotamento é concluído, a chave de empacotamento é coletada pelo lixo e não é explicitamente destruída. Como resultado, a chave de empacotamento permanece presente na memória por algum tempo. Você deve se proteger contra o acesso não autorizado à máquina e garantir que não exponha nenhum arquivo, como dumps principais, que possam revelar essas informações.

## Armazenando políticas com segurança {#securely-storing-policies}

O SDK do Adobe Primetime DRM permite desenvolver aplicativos que podem ser usados em pacotes de conteúdo e criação de políticas.

Ao criar esses aplicativos, você pode permitir que alguns usuários criem e modifiquem políticas e limitar outros usuários a aplicar somente políticas existentes ao conteúdo. Você deve implementar os controles de acesso necessários e criar contas de usuário com privilégios diferentes para a criação de políticas e a aplicação de políticas.

As políticas não são assinadas ou protegidas contra modificações até que sejam usadas no pacote. Se você estiver preocupado que os usuários da ferramenta de empacotamento possam modificar as políticas, assine as políticas para garantir que elas não possam ser modificadas.

Para obter mais informações sobre como criar aplicativos com o SDK, consulte as APIs do Primetime DRM em [Referências da API Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## Criptografia de chave assimétrica {#asymmetric-key-encryption}

A criptografia de chave assimétrica, também chamada de criptografia de chave pública, usa pares de chaves. Uma chave é para criptografia, e a outra é para descriptografia.

A chave de descriptografia ou a variável *`private key`*, é mantido em segredo; a chave de criptografia ou a variável *`public key`* O, é disponibilizado a qualquer pessoa autorizada a criptografar conteúdo. Qualquer pessoa com acesso à chave pública pode criptografar o conteúdo. No entanto, somente alguém com acesso à chave privada pode descriptografar o conteúdo. A chave privada não pode ser reconstruída a partir da chave pública.

Ao criar o pacote do conteúdo, a chave pública do License Server é usada para criptografar a chave de criptografia do conteúdo (CEK) nos metadados de DRM. Você deve garantir que somente o License Server tenha acesso à chave privada do License Server. Se outra pessoa tiver a chave, poderá descriptografar e visualizar o conteúdo.

>[!CAUTION]
>
>Obtenha o certificado do License Server que inclui a chave pública de uma fonte confiável. Dessa forma, você pode garantir que seja a chave do License Server e não uma chave pública não autorizada. Se os invasores substituíssem a chave pública pela chave do License Server, eles poderiam descriptografar o conteúdo.

Para obter mais informações sobre como criar um pacote de conteúdo, consulte [Utilização do SDK do Adobe Primetime DRM para proteção de conteúdo](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).
