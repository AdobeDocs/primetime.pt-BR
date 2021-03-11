---
title: Embalagem segura
description: Embalagem segura
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Empacotar conteúdo com segurança {#securely-packaging-content}

O arquivo de configuração para a ferramenta de linha de comando Adobe Access Media Packager requer uma credencial PKCS12 usada durante o empacotamento.

Nas ferramentas de Linha de Comando de Implementação de Referência, a senha do arquivo de credenciais PKCS12 é armazenada no arquivo flashaccess.properties em texto limpo. Por isso, tenha cuidado ao proteger o computador que hospeda esse arquivo e garantir que ele esteja em um ambiente seguro. (Consulte [Segurança física e acesso](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

O empacotador também usa os certificados de Transporte do License Server e do License Server. A integridade e a confidencialidade destas informações devem ser protegidas. Só as entidades autorizadas devem ser autorizadas a utilizar o embalador. Se alguma de suas chaves privadas estiver comprometida, informe imediatamente o Adobe Systems Incorporated para que o certificado possa ser revogado.

>[!NOTE]
>
>A API permite usar a mesma chave para vários conteúdos. Para garantir o mais alto nível de segurança, recomendamos que esse recurso seja usado apenas para conteúdo FMS de taxa de bits múltipla. Não é recomendado usar a mesma chave para vários arquivos que representam conteúdo diferente.

A API de empacotamento de acesso ao Adobe emite avisos sob determinadas condições. Você deve revisar esses avisos para determinar se os arquivos foram criptografados com êxito. As mensagens de aviso podem indicar que a política expirou, uma tag ou rastreamento não reconhecido não será criptografado, os fragmentos de filme não serão criptografados (e as referências nesses fragmentos podem se tornar inválidas) e os metadados não serão criptografados.

Se o conteúdo for empacotado usando uma política com atributos incorretos, a política deverá ser atualizada e a política atualizada deverá ser disponibilizada ao License Server por meio de uma lista de atualização de política ou outro mecanismo para fornecer a política atualizada ao servidor. Alguns atributos de política não podem ser alterados após a criação da política. Se esses atributos estiverem incorretos, puxe o conteúdo de volta dos sites de distribuição, revogue a política para que nenhuma licença futura possa ser concedida e criptografe novamente o conteúdo.

Quando a embalagem estiver completa, a chave de embalagem não é explicitamente destruída; no entanto, é coletado lixo. Por conseguinte, a chave de embalagem permanece na memória por um período de tempo; você deve proteger contra acesso não autorizado à máquina e tomar medidas para garantir que não exponha arquivos, como despejos principais, que possam revelar essas informações.
