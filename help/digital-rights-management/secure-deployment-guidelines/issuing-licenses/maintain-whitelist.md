---
description: Uma lista de permissões é uma lista de entidades confiáveis.
title: Mantenha uma lista de permissões de empacotadores de conteúdo confiáveis
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Mantenha uma lista de permissões de empacotadores de conteúdo confiáveis {#maintain-a-allowlist-of-trusted-content-packagers}

Uma lista de permissões é uma lista de entidades confiáveis.

Para os empacotadores de conteúdo, as entidades são organizações nas quais o proprietário do conteúdo confia para empacotar (ou criptografar) os arquivos de vídeo e criar conteúdo protegido por DRM. Ao implantar o Adobe Primetime DRM, você deve manter uma lista de permissões de compactadores de conteúdo confiáveis. Você também deve verificar a identidade do empacotador de conteúdo nos metadados de DRM de um arquivo protegido por DRM antes de emitir uma licença.

Para saber como obter informações sobre a entidade que compactou o conteúdo, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
