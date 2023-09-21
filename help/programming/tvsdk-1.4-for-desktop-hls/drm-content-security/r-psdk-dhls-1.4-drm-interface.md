---
description: O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais (DRM) do Primetime é o Gerenciador de DRM.
title: Visão geral da interface DRM do Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Visão geral da interface DRM do Primetime{#primetime-drm-interface-overview}

O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais (DRM) do Primetime é o Gerenciador de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

O TVSDK oferece suporte à integração DRM do Primetime como fluxos de trabalho DRM personalizados. Isso significa que o aplicativo deve implementar os workflows de autenticação DRM antes de reproduzir o fluxo usando o Flash `DRMManager`. Para habilitar isso, a variável `MediaPlayer` O fornece o gerenciador DRM para autenticação.

Estes são os elementos de API mais importantes para trabalhar com DRM:

* Uma referência no reprodutor de mídia ao objeto gerenciador de DRM que implementa o subsistema de DRM:

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
