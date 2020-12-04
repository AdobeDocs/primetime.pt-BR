---
seo-title: Manter uma lista de permissões de pacotes de conteúdo confiável
title: Manter uma lista de permissões de pacotes de conteúdo confiável
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Manter uma lista de permissões de pacotes de conteúdo confiável {#maintain-a-allowlist-of-trusted-content-packagers}

Uma **lista de permissões** é uma lista de entidades confiáveis. No caso de pacotes de conteúdo, essas organizações são confiáveis pelo proprietário do conteúdo para disponibilizar (ou criptografar) os arquivos de vídeo FLV/F4V, criando conteúdo protegido por DRM. Ao implantar o Adobe Access, é recomendável manter uma lista de permissões de pacotes de conteúdo confiáveis e verificar a identidade do pacote de conteúdo contido nos metadados DRM (cabeçalho DRM) de um arquivo protegido por DRM antes de emitir uma licença.

Para saber mais sobre como obter informações sobre a entidade que empacotou o conteúdo, consulte `V2ContentMetaData.getPackagerInfo()` na *Referência da API de Acesso ao Adobe*.
