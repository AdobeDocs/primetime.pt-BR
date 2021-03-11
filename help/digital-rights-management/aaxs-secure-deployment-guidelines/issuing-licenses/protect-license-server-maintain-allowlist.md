---
title: Manter uma lista de permissões de pacotes de conteúdo confiáveis
description: Manter uma lista de permissões de pacotes de conteúdo confiáveis
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Manter uma lista de permissões de pacotes de conteúdo confiáveis {#maintain-a-allowlist-of-trusted-content-packagers}

Uma **lista de permissões** é uma lista de entidades confiáveis. No caso de pacotes de conteúdo, essas são organizações confiáveis pelo proprietário do conteúdo para empacotar (ou criptografar) os arquivos de vídeo FLV/F4V, criando conteúdo protegido por DRM. Ao implantar o Adobe Access, é recomendável manter uma lista de permissões de pacotes de conteúdo confiáveis e verificar a identidade do pacote de conteúdo contido nos metadados DRM (o cabeçalho DRM) de um arquivo protegido por DRM antes de emitir uma licença.

Para saber mais sobre como obter informações sobre a entidade que empacotou o conteúdo, consulte `V2ContentMetaData.getPackagerInfo()` no *Referência da API de acesso ao Adobe*.
