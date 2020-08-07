---
seo-title: Conteúdo de empacotamento seguro
title: Conteúdo de empacotamento seguro
uuid: a5e7cc17-353b-47d1-b89c-a2ba3c9faca1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Conteúdo de empacotamento seguro {#securely-packaging-content}

O arquivo de configuração da ferramenta de linha de comando do Adobe Access Media Packager requer uma credencial PKCS12 usada durante o empacotamento.

Nas ferramentas de Linha de Comando de Implementação de Referência, a senha para o arquivo de credenciais PKCS12 é armazenada no arquivo flashaccess.properties em texto limpo. Por esse motivo, tenha cuidado extra ao proteger o computador que hospeda esse arquivo e verifique se ele está em um ambiente seguro. (Consulte Segurança [física e acesso](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

O empacotador também usa os certificados de Transporte do License Server e do License Server. Tanto a integridade como a confidencialidade destas informações devem ser protegidas. Só as entidades autorizadas devem ser autorizadas a utilizar o embalador. Se alguma de suas chaves privadas estiver comprometida, informe imediatamente a Adobe Systems Incorporated para que o certificado possa ser revogado.

>[!NOTE]
>
>A API permite que você use a mesma chave para vários conteúdos. Para garantir o mais alto nível de segurança, recomendamos que esse recurso seja usado apenas para conteúdo FMS de taxa de vários bits. Não é recomendável usar a mesma chave para vários arquivos que representam conteúdo diferente.

A API de empacotamento de acesso ao Adobe emite avisos sob determinadas condições. É necessário revisar esses avisos para determinar se os arquivos foram criptografados com êxito. As mensagens de aviso podem indicar que a política expirou, que uma tag ou rastreamento não reconhecido não será criptografado, que os fragmentos de filme não serão criptografados (e as referências nesses fragmentos podem se tornar inválidas) e que os metadados não serão criptografados.

Se o conteúdo for empacotado usando uma política com atributos incorretos, a política deverá ser atualizada e a política atualizada deverá ser disponibilizada ao License Server por meio de uma lista de atualização de política ou outro mecanismo para fornecer a política atualizada ao servidor. Alguns atributos de política não podem ser alterados depois que a política é criada. Se esses atributos estiverem incorretos, extraia o conteúdo dos sites de distribuição, revogue a política para que nenhuma licença futura possa ser concedida e criptografe novamente o conteúdo.

Quando a embalagem estiver completa, a chave de embalagem não é explicitamente destruída; no entanto, é coletada de lixo. Por conseguinte, a chave de embalagem permanece presente na memória durante um período de tempo; você deve se proteger contra o acesso não autorizado ao computador e tomar medidas para garantir que não exponha quaisquer arquivos, como os lixões principais, que possam revelar essas informações.
