---
description: O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais Primetime (DRM) é o Gerenciador de DRM.
seo-description: O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais Primetime (DRM) é o Gerenciador de DRM.
seo-title: Visão geral da interface do Primetime DRM
title: Visão geral da interface do Primetime DRM
uuid: 3aae7c7a-fd0c-430e-9018-fd72801ab778
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b

---


# Visão geral da interface do Primetime DRM {#primetime-drm-interface-overview}

Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução de DRM Primetime integrada da Adobe.

Consulte seu representante da Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais Primetime (DRM) é o Gerenciador de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao seu conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

O TVSDK oferece suporte à integração de DRM Primetime como fluxos de trabalho de DRM personalizados. Isso significa que seu aplicativo deve implementar os fluxos de trabalho de autenticação DRM antes de reproduzir o fluxo usando o Flash DRMManager. Para habilitar isso, o MediaPlayer fornece o gerenciador de DRM para autenticação.

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

>[!TIP] {important=&quot;high&quot;}
>
>Ao referenciar URLs de ativos protegidos por DRM no aplicativo iOS, o parâmetro da string de consulta `?faxs=1` deve ser anexado ao URL M3U8 de nível definido (MBR). Por exemplo: >
>
```>
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```>
>The `faxs=1` query string parameter signals that the content is DRM protected, and triggers the DRM decryption workflow accordingly in the iOS TVSDK. You can also append the `faxs=1` tag on DRM-protected HLS asset URLs that are destined for other platforms; it is observed as required on iOS or treated as a non-op in players on other platforms.



<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obter mais informações sobre o DRM, consulte a documentação [do](https://help.adobe.com/en_US/primetime/drm)Adobe Primetime DRM.

## Implementação do Primetime DRM em um aplicativo TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

O Primetime DRM é integrado ao TVSDK, o que simplifica a implementação da proteção de conteúdo em um aplicativo TVSDK.

Para obter uma visão geral e detalhes sobre como usar o Primetime DRM para implementar a proteção de conteúdo em um aplicativo TVSDK, consulte:

* [Fluxo de trabalho do Adobe Primetime TVSDK-DRM (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)