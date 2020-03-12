---
description: Uma lista de permissões é uma lista de entidades confiáveis.
seo-description: Uma lista de permissões é uma lista de entidades confiáveis.
seo-title: Manter uma lista de permissões de pacotes de conteúdo confiáveis
title: Manter uma lista de permissões de pacotes de conteúdo confiáveis
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Manter uma lista de permissões de pacotes de conteúdo confiáveis{#maintain-a-whitelist-of-trusted-content-packagers}

Uma lista de permissões é uma lista de entidades confiáveis.

Para os empacotadores de conteúdo, as entidades são organizações confiáveis pelo proprietário do conteúdo para disponibilizar (ou criptografar) os arquivos de vídeo e criar conteúdo protegido por DRM. Ao implantar o Adobe Primetime DRM, você deve manter uma lista de permissões de pacotes de conteúdo confiáveis. Você também deve verificar a identidade do empacotador de conteúdo nos metadados DRM de um arquivo protegido por DRM antes de emitir uma licença.

Para saber como obter informações sobre a entidade que empacotou o conteúdo, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
