---
description: Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução de DRM integrada do Primetime com Adobe.
keywords: DRM;DASH;HLS
seo-description: Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução de DRM integrada do Primetime com Adobe.
seo-title: Visão geral da interface do Primetime DRM
title: Visão geral da interface do Primetime DRM
uuid: 5e794147-cc58-448c-b8ec-065e80ef01fd
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# Visão geral da interface do Primetime DRM {#primetime-drm-interface-overview}

Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução de DRM integrada do Primetime com Adobe.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Consulte seu representante de Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais Primetime (DRM) é o Gerenciador de DRM.

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao seu conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

O TVSDK suporta a integração do Primetime DRM como workflows DRM personalizados. Isso significa que seu aplicativo deve implementar os workflows de autenticação DRM antes de reproduzir o fluxo usando o Flash DRMManager. Para habilitar isso, o MediaPlayer fornece o gerenciador de DRM para autenticação.

Consulte o código do player de amostra de DRM incluído no pacote TVSDK.

Esses são os elementos de API mais importantes para trabalhar com DRM:

* Uma referência no player de mídia ao objeto do gerenciador DRM que implementa o subsistema DRM:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

O TVSDK emite uma `PTMediaPlayerItemDRMMetadataChanged` notificação quando os metadados do DRM são alterados. Esses metadados são usados como entrada para quase todas as funções da `DRMManager` classe.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Se o fluxo protegido por DRM estiver codificado com várias taxas de bits (MBR), os metadados de DRM usados para a lista de reprodução variante devem ser os mesmos que os metadados usados em todos os fluxos de taxa de bits.

>[!TIP]
>
>Ao fazer referência a URLs de ativos protegidos por DRM no aplicativo iOS, o parâmetro da string de query `?faxs=1` deve ser anexado ao URL M3U8 de nível definido (MBR). Por exemplo:

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

O parâmetro da string de `faxs=1` query indica que o conteúdo está protegido por DRM e aciona o fluxo de trabalho de decodificação de DRM de acordo com o TVSDK do iOS. Você também pode anexar a `faxs=1` tag em URLs de ativos HLS protegidos por DRM destinados a outras plataformas; é observado conforme necessário no iOS ou tratado como não operacional em players em outras plataformas.

## Implementação do Primetime DRM em um aplicativo TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

O Primetime DRM é integrado ao TVSDK, o que simplifica a implementação da proteção de conteúdo em um aplicativo TVSDK.

Para obter uma visão geral e detalhes sobre como usar o Primetime DRM para implementar a proteção de conteúdo em um aplicativo TVSDK, consulte:

* [Fluxo de trabalho do Adobe Primetime TVSDK-DRM (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)