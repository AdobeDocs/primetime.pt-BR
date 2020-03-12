---
seo-title: Manter uma lista de permissões de pacotes de conteúdo confiáveis
title: Manter uma lista de permissões de pacotes de conteúdo confiáveis
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Manter uma lista de permissões de pacotes de conteúdo confiáveis{#maintain-a-whitelist-of-trusted-content-packagers}

Uma lista *branca* é uma lista de entidades confiáveis. No caso de pacotes de conteúdo, essas organizações são confiáveis pelo proprietário do conteúdo para disponibilizar (ou criptografar) os arquivos de vídeo FLV/F4V, criando conteúdo protegido por DRM. Ao implantar o Adobe Access, é recomendável manter uma lista de permissões de pacotes de conteúdo confiáveis e verificar a identidade do pacote de conteúdo contido nos metadados DRM (cabeçalho DRM) de um arquivo protegido por DRM antes de emitir uma licença.

Para saber mais sobre como obter informações sobre a entidade que empacotou o conteúdo, consulte `V2ContentMetaData.getPackagerInfo()` a Referência *da API do* Adobe Access.
