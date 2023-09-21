---
title: Empacotando conteúdo com segurança
description: Empacotando conteúdo com segurança
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Empacotando conteúdo com segurança {#securely-packaging-content}

O arquivo de configuração da ferramenta de linha de comando Adobe Access Media Packager requer uma credencial PKCS12 usada durante o empacotamento.

Nas ferramentas de Linha de Comando de Implementação de Referência, a senha do arquivo de credenciais PKCS12 é armazenada no arquivo flashaccess.properties em texto simples. Por esse motivo, tenha cuidado extra ao proteger o computador que hospeda esse arquivo e verifique se ele está em um ambiente seguro. (Consulte [Segurança física e acesso](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

O empacotador também usa os certificados de Transporte do Servidor de Licenças e do Servidor de Licenças. A integridade e a confidencialidade dessas informações devem ser protegidas. Apenas as entidades autorizadas devem ser autorizadas a utilizar o acondicionador. Se alguma de suas chaves privadas estiver comprometida, informe imediatamente o Adobe Systems Incorporated para que o certificado possa ser revogado.

>[!NOTE]
>
>A API permite usar a mesma chave para vários conteúdos. Para garantir o mais alto nível de segurança, recomendamos que esse recurso seja usado somente para conteúdo FMS com taxa de vários bits. Não é recomendável usar a mesma chave para vários arquivos que representam conteúdo diferente.

A API de empacotamento de acesso ao Adobe emite avisos sob determinadas condições. Você deve revisar esses avisos para determinar se os arquivos foram criptografados com êxito. As mensagens de aviso podem indicar que a política expirou, que uma tag ou trilha não reconhecida não será criptografada, que os fragmentos de filme não serão criptografados (e que as referências dentro desses fragmentos podem se tornar inválidas) e que os metadados não serão criptografados.

Se o conteúdo for empacotado usando uma política com atributos incorretos, a política deverá ser atualizada e a política atualizada deverá ser disponibilizada ao License Server por meio de uma lista de atualização de política ou outro mecanismo para fornecer a política atualizada ao servidor. Alguns atributos de política não podem ser alterados após a criação da política. Se esses atributos estiverem incorretos, obtenha o conteúdo dos sites de distribuição, revogue a política para que nenhuma licença futura possa ser concedida e criptografe novamente o conteúdo.

Quando o empacotamento é concluído, a chave de empacotamento não é explicitamente destruída; no entanto, ela é coletada pelo lixo. Portanto, a chave de empacotamento permanece na memória por um período de tempo; você deve proteger contra acesso não autorizado à máquina e tomar medidas para garantir que não exponha nenhum arquivo, como despejos de núcleo, que possam revelar essas informações.
