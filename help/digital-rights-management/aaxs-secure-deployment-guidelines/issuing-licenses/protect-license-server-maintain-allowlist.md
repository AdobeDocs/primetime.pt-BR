---
title: Mantenha uma lista de permissões de empacotadores de conteúdo confiáveis
description: Mantenha uma lista de permissões de empacotadores de conteúdo confiáveis
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Mantenha uma lista de permissões de empacotadores de conteúdo confiáveis {#maintain-a-allowlist-of-trusted-content-packagers}

Um **lista de permissões** é uma lista de entidades confiáveis. No caso dos empacotadores de conteúdo, essas são organizações nas quais o proprietário do conteúdo confia para empacotar (ou criptografar) os arquivos de vídeo FLV/F4V, criando conteúdo protegido DRM. Ao implantar o Adobe Access, é recomendável manter uma lista de permissões de compactadores de conteúdo confiáveis e verificar a identidade do compactador de conteúdo contido nos metadados de DRM (o cabeçalho DRM) de um arquivo protegido por DRM antes de emitir uma licença.

Para saber mais sobre como obter informações sobre a entidade que compactou o conteúdo, consulte `V2ContentMetaData.getPackagerInfo()` no *Referência da API de acesso do Adobe*.
