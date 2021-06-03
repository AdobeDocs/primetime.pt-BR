---
title: Notas de versão do Primetime
description: Notas de versão do Primetime
copied-description: true
exl-id: 29087a3e-f16e-4510-8d3a-ed2229700899
source-git-commit: fe0f5f3399d2e2ab3e07713fbcd29ede47888d98
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 31%

---

# Notas de versão do Primetime

Bem-vindo às Notas de versão da Adobe Primetime. Os documentos listados na navegação à esquerda fornecem informações específicas da versão, requisitos do sistema, limitações, problemas corrigidos e problemas conhecidos.

## Melhorias e correções no PTAI 21.5.1

A versão inclui nova telemetria para alterações futuras do painel e suporte para a segmentação obsoleta tipo 0x01 (UPID) para formatos de sinalização baseados em SCTE.

Para outras correções e detalhes, consulte [Notas de versão do Ad Insertion](/help/release-notes/ptai-21x-release-notes.md)

## Aprimoramentos e correções no TVSDK 3.13 iOS

A versão apresenta suporte para anúncios DEMUXED &#39;HLS/CMAF&#39; (pré-lançamento, midroll e postroll) para fluxos LIVE, VOD e FER.

Para outras correções e detalhes, consulte [TVSDK para Notas de versão do iOS](../release-notes/tvsdk-3x-ios.md)

## Correções no TVSDK 3.13 Android

Esta versão oferece uma solução alternativa para o problema sobre o congelamento do fluxo de DRM da Widevine ou a exibição de quadros pretos no switch ABR em dispositivos FireTV, que incluem Fire TV Pendant e Fire TV Fogo Cube 1ª e 2ª geração de dispositivos.

Para resolver o problema, defina a API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` para os dispositivos Fire TV especificados antes de iniciar a reprodução. O valor padrão é false.

Consulte as [TVSDK para Notas de versão do Android](../release-notes/tvsdk-3x-android.md) para obter mais informações.

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
