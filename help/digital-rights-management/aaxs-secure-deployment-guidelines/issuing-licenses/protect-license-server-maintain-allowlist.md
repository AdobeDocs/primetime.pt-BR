---
seo-title: Manter uma lista permitida de pacotes de conteúdo confiável
title: Manter uma lista permitida de pacotes de conteúdo confiável
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Manter uma lista permitida de pacotes de conteúdo confiável{#maintain-a-allowlist-of-trusted-content-packagers}

Uma lista *permitida* é uma lista de entidades confiáveis. No caso de pacotes de conteúdo, essas organizações são confiáveis pelo proprietário do conteúdo para disponibilizar (ou criptografar) os arquivos de vídeo FLV/F4V, criando conteúdo protegido por DRM. Ao implantar o Adobe Access, é recomendável manter uma lista permitida de pacotes de conteúdo confiáveis e verificar a identidade do pacote de conteúdo contido nos metadados DRM (cabeçalho DRM) de um arquivo protegido por DRM antes de emitir uma licença.

Para saber mais sobre como obter informações sobre a entidade que empacotou o conteúdo, consulte `V2ContentMetaData.getPackagerInfo()` a Referência *da API do* Adobe Access.
