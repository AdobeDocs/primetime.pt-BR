---
description: O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais Primetime (DRM) é o Gerenciador de DRM.
seo-description: O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais Primetime (DRM) é o Gerenciador de DRM.
seo-title: Visão geral da interface do Primetime DRM
title: Visão geral da interface do Primetime DRM
uuid: 01714ee6-a937-4ca3-b535-6a6ef681ee6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Visão geral da interface do Primetime DRM{#primetime-drm-interface-overview}

O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais Primetime (DRM) é o Gerenciador de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao seu conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

O TVSDK oferece suporte à integração de DRM Primetime como fluxos de trabalho de DRM personalizados. Isso significa que seu aplicativo deve implementar os fluxos de trabalho de autenticação DRM antes de reproduzir o fluxo usando o Flash `DRMManager`. Para habilitar isso, o `MediaPlayer` fornece o gerenciador DRM para autenticação.

Esses são os elementos de API mais importantes para trabalhar com DRM:

* Uma referência no player de mídia ao objeto do gerenciador DRM que implementa o subsistema DRM:

   ```
   public function get drmManager():DRMManager 
   ```

<!--<a id="section_4204CE2731A44F67A3664AEDE8CCCA47"></a>-->

Elementos adicionais relevantes da API:

* [flash.net.drm.DRMManager](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html)
* [flash.net.drm.DRMContentData](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMContentData.html)
* [flash.net.drm.DRMVoucher](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMVoucher.html)
* [flash.net.drm.AuthenticationMethod](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/AuthenticationMethod.html)
* [flash.events.DRMStatusEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMStatusEvent.html)
* [flash.events.DRMErrorEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMErrorEvent.html)

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obter mais informações sobre o DRM, consulte a documentação do Adobe Primetime DRM.
