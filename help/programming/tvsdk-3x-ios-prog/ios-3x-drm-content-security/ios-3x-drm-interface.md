---
description: Você pode usar os recursos do sistema de Digital Rights Management do Primetime (DRM) para fornecer acesso seguro ao conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa para a solução de DRM Primetime integrada do Adobe.
keywords: DRM;DASH;HLS
title: Visão geral da interface DRM do Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Visão geral da interface DRM do Primetime {#primetime-drm-interface-overview}

Você pode usar os recursos do sistema de Digital Rights Management do Primetime (DRM) para fornecer acesso seguro ao conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa para a solução de DRM Primetime integrada do Adobe.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Consulte seu representante de Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais (DRM) do Primetime é o Gerenciador de DRM.

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

O TVSDK oferece suporte à integração DRM do Primetime como fluxos de trabalho DRM personalizados. Isso significa que o aplicativo deve implementar os workflows de autenticação DRM antes de reproduzir o fluxo usando o Flash DRManager. Para ativar isso, o MediaPlayer fornece o gerenciador de DRM para autenticação.

Consulte o código do reprodutor de amostra DRM incluído no pacote TVSDK.

Estes são os elementos de API mais importantes para trabalhar com DRM:

* Uma referência no reprodutor de mídia ao objeto gerenciador de DRM que implementa o subsistema de DRM:

  ```
  @property (readonly, nonatomic) DRMManager *drmManager
  ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

O TVSDK emite um `PTMediaPlayerItemDRMMetadataChanged` quando os metadados de DRM são alterados. Esses metadados são usados como entrada para quase todas as funções da `DRMManager` classe.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Se o fluxo protegido por DRM estiver codificado com taxa de bits múltipla (MBR), os metadados de DRM usados para a lista de reprodução da variante deverão ser os mesmos que os metadados usados em todos os fluxos de taxa de bits.

>[!TIP]
>
>Ao referenciar URLs de ativos protegidos por DRM no aplicativo iOS, o parâmetro da sequência de consulta `?faxs=1` deve ser anexado ao URL M3U8 de nível de conjunto (MBR). Por exemplo:

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

A variável `faxs=1` O parâmetro da sequência de consulta indica que o conteúdo está protegido por DRM e aciona o fluxo de trabalho de descriptografia DRM de acordo com o TVSDK do iOS. Também é possível anexar a variável `faxs=1` tag em URLs de ativos HLS protegidos por DRM que são destinados a outras plataformas; é observada conforme necessário no iOS ou tratada como não operacional em players em outras plataformas.

## Implementar o Primetime DRM em um aplicativo TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

O Primetime DRM é integrado ao TVSDK, o que simplifica a implementação da proteção de conteúdo em um aplicativo TVSDK.

Para obter uma visão geral e detalhes sobre o uso do Primetime DRM para implementar a proteção de conteúdo em um aplicativo TVSDK, consulte:

* [Fluxo de trabalho Adobe Primetime TVSDK-DRM (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
