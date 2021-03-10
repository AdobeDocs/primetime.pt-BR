---
description: O elemento principal do lado do cliente do sistema Primetime digital rights management (DRM) é o Gerenciador de DRM.
title: Visão geral da interface DRM do Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# Visão geral da interface DRM do Primetime {#primetime-drm-interface-overview}

Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao conteúdo de vídeo. Como alternativa, você pode usar soluções DRM de terceiros como uma alternativa para a solução DRM integrada do Primetime Adobe.

Consulte seu representante de Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

O elemento principal do lado do cliente do sistema Primetime digital rights management (DRM) é o Gerenciador de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

O TVSDK oferece suporte à integração de DRM do Primetime como fluxos de trabalho de DRM personalizados. Isso significa que o aplicativo deve implementar os workflows de autenticação de DRM antes de reproduzir o fluxo usando o Flash DRMManager. Para habilitar isso, o MediaPlayer fornece o gerenciador de DRM para autenticação.

Consulte o código do reprodutor de amostra DRM incluído no pacote TVSDK.

Esses são os elementos de API mais importantes para trabalhar com DRM:

* Uma referência no reprodutor de mídia ao objeto do gerenciador de DRM que implementa o subsistema de DRM:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

O TVSDK emite uma notificação `PTMediaPlayerItemDRMMetadataChanged` quando os metadados do DRM são alterados. Esses metadados são usados como entrada para quase todas as funções da classe `DRMManager`.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Se o fluxo protegido por DRM estiver codificado com várias taxas de bits (MBR), os metadados de DRM usados para a lista de reprodução da variante devem ser iguais aos metadados usados em todos os fluxos de taxa de bits.

>[!TIP]
>
>Ao fazer referência a URLs de ativos protegidos por DRM no aplicativo iOS, o parâmetro da string de consulta `?faxs=1` deve ser anexado ao URL M3U8 no nível de conjunto (MBR). Por exemplo:
>
>
```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>O parâmetro da sequência de consulta `faxs=1` indica que o conteúdo está protegido por DRM e dispara o fluxo de trabalho de descriptografia de DRM de acordo com o TVSDK do iOS. Você também pode anexar a tag `faxs=1` em URLs de ativos HLS protegidos por DRM que são destinados a outras plataformas; é observado conforme necessário no iOS ou tratado como não operacional em players em outras plataformas.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obter mais informações sobre DRM, consulte a [documentação do DRM Adobe Primetime](https://help.adobe.com/en_US/primetime/drm).

## Implementar o Primetime DRM em um aplicativo TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

O DRM do Primetime é integrado ao TVSDK, o que simplifica a implementação da proteção de conteúdo em um aplicativo TVSDK.

Para obter uma visão geral e detalhes sobre como usar o DRM do Primetime para implementar a proteção de conteúdo em um aplicativo TVSDK, consulte:

* [Fluxo de trabalho TVSDK-DRM do Adobe Primetime (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)