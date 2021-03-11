---
description: Uma lista de permissões é uma lista de entidades confiáveis.
title: Manter uma lista de permissões de pacotes de conteúdo confiáveis
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Manter uma lista de permissões de pacotes de conteúdo confiáveis {#maintain-a-allowlist-of-trusted-content-packagers}

Uma lista de permissões é uma lista de entidades confiáveis.

Para pacotes de conteúdo, as entidades são organizações confiáveis pelo proprietário do conteúdo para empacotar (ou criptografar) os arquivos de vídeo e criar conteúdo protegido por DRM. Ao implantar o Adobe Primetime DRM, você deve manter uma lista de permissões de pacotes de conteúdo confiáveis. Você também deve verificar a identidade do pacote de conteúdo nos metadados DRM de um arquivo protegido por DRM antes de emitir uma licença.

Para saber como obter informações sobre a entidade que empacotou o conteúdo, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
