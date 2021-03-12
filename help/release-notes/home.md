---
title: Notas de versão do Primetime
description: Notas de versão do Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 944bfb0f3bd0050a9d2974a37f4fabddaaac8a93
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 29%

---


# Notas de versão do Primetime

Bem-vindo às Notas de versão da Adobe Primetime. Os documentos listados na navegação à esquerda fornecem informações específicas da versão, requisitos do sistema, limitações, problemas corrigidos e problemas conhecidos.

## Aprimoramentos e correções no TVSDK 3.13 iOS

A versão apresenta suporte para anúncios DEMUXED &#39;HLS/CMAF&#39; (pré-lançamento, midroll e postroll) para fluxos LIVE, VOD e FER.

Para outras correções e detalhes, consulte [TVSDK para Notas de versão do iOS](../release-notes/tvsdk-3x-ios.md)

## Melhorias e correções no PTAI 21.2.2

A versão inclui suporte para inserção/sincronização de fluxo EXT-X-IMAGE-STREAM-INF em fluxos HLS. O recurso é ativado por meio de uma configuração do lado do servidor. Entre em contato com seu representante de conta técnica para ativar o recurso.

## Correções no TVSDK 3.13 Android

Esta versão oferece uma solução alternativa para o problema sobre o congelamento do fluxo de DRM da Widevine ou a exibição de quadros pretos no switch ABR em dispositivos FireTV, que incluem Fire TV Pendant e Fire TV Fogo Cube 1ª e 2ª geração de dispositivos.

Para resolver o problema, defina a API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` para os dispositivos Fire TV especificados antes de iniciar a reprodução. O valor padrão é false.

Consulte as [TVSDK para Notas de versão do Android](../release-notes/tvsdk-3x-android.md) para obter mais informações.

## Melhorias e correções nas Notas de versão do TVSDK 3.12 iOS

A versão do se concentrava na solução dos principais problemas do cliente.

Consulte para obter mais informações sobre a versão lançada atual para [iOS](../release-notes/tvsdk-3x-ios.md).

## Consulte também

| Guia do usuário | Descrição |
|--- |--- |
| [Ajuda da programação do Primetime](/help/programming/home.md) | Com ele, você aprende a desenvolver aplicativos e reprodutores de vídeo usando Java em dispositivos Android e em dispositivos Objective-C em iOS. |
| [Ajuda da migração e conversão do Primetime](/help/migration-guides/home.md) | Explica o processo de conversão e migração para migrar do Primetime TVSDK Suite existente para uma da próxima geração. |
| [Implementação de referência](/help/android-reference-implementation/home.md) | Ajuda a entender o TVSDK e modificar os gerentes de recursos para personalizar o seu reprodutor pessoal. |
| [Referências da API do Primetime](/help/reference/api-references.md) | Fornece informações detalhadas sobre as funções do TVSDK, estruturas de dados e outras construções de programação. |
| [Digital Rights Management](/help/digital-rights-management/home.md) | Ajuda você a saber mais sobre vários cenários de usuário no Digital Rights Management (DRM) |
| [Ajuda do Primetime Ad Insertion](/help/primetime-ad-insertion/home.md) | Explica como monetizar o conteúdo inserindo anúncios dinâmicos direcionados ao usuário no servidor e engajar o público-alvo com anúncios personalizados. |
| [Arquivos](https://helpx.adobe.com/primetime/archives.html) | Baixe PDFs da documentação arquivada. |

## Recursos úteis

* [Noções básicas sobre o Adobe Primetime](https://www.adobe.com/in/marketing/primetime.html)

* [Monitoramento de simultaneidade](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)

* [Autenticação do Primetime](https://tve.helpdocsonline.com/home)

* [Fóruns de DRM da Adobe Primetime](https://forums.adobe.com/community/adobe_access)

* [Recursos do desenvolvedor do Adobe Primetime](https://www.adobe.com/devnet/primetime.html)
