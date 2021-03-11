---
description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
title: Métodos MediaPlayerItem para acessar informações do MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Métodos MediaPlayerItem para acessar as informações do MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.

| Método | Descrição |
|--- |--- |
| **Tags de anúncio** |  |
| List`<String>` getAdTags() | Fornece a lista de tags de anúncio usadas para o processo de posicionamento do anúncio. |
| **Live stream** |  |
| booleano isLive(); | Verdadeiro se o fluxo for em tempo real; falso se for VOD. |
| **DRM protegido** |  |
| booleano isProtected(); | Verdadeiro se o fluxo estiver protegido por DRM. |
| List`<DRMMetadataInfo>` getDRMMetadataInfos(); | Lista todos os objetos de metadados DRM detectados no manifesto. |
| **Legendas ocultas** |  |
| booleano hasClosedCaptions(); | True se as faixas de legenda fechada estiverem disponíveis. |
| List`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Fornece uma lista de faixas de legendas ocultas disponíveis. |
| ClosedCaptionsTrack get SeletedClosedCaptionsTrack(); | Recupera o rastreamento de legenda fechada atual selecionado com SelectClosedCaptionsTrack . |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | Define uma faixa de legenda fechada para ser a faixa de legenda fechada atual. |
| **Trilhas de áudio alternativas** |  |
| booleano hasAlternateAudio(); | True é verdadeiro se o fluxo tiver trilhas de áudio alternativas. Observação:  A faixa de áudio principal (padrão) também faz parte da lista de faixa de áudio alternativa.  O TVSDK para Android considera a faixa de áudio principal um dos itens na lista de faixa de áudio alternativa. Por causa disso, o único caso em que MediaPlayerItem.hasAlternateAudio retorna false é quando o fluxo não tem nenhum áudio. Se o conteúdo tiver apenas uma faixa de áudio, esse método retornará true e `MediaPlayerItem.getAudioTracks` retornará uma lista com um único elemento (a faixa de áudio padrão). |
| List`<AudioTrack>` getAudioTracks(); | Fornece uma lista de trilhas de áudio alternativas disponíveis. |
| AudioTrack getSeletedAudioTrack(); | Recupera a faixa de áudio selecionada com selectAudioTrack . |
| selectAudioTrack ( AudioTrack audioTrack ) | Seleciona uma faixa de áudio para ser a faixa de áudio atual. |
| **Metadados cronometrados** |  |
| booleano hasTimedMetadata(); | True se o fluxo tiver metadados cronometrados associados. |
| List`<TimedMetadata>` getTimedMetadata(); | Fornece uma lista dos objetos de metadados cronometrados associados ao fluxo. |
| **Vários perfis (taxas de bits)** |
| booleano isDynamic(); | True se o fluxo for um fluxo de taxa de bits múltipla (MBR). |
| List`<Profile>` getProfiles(); | Fornece uma lista dos perfis de taxa de bits associados. Para cada perfil, você pode recuperar sua taxa de bits e a altura e a largura do perfil. |
| Perfil getSeletedProfile() | Recupera o perfil selecionado no momento. |
| **Trick Play** |  |
| booleano isTrickPlaySupported(); | Verdadeiro se o reprodutor suportar avançar, retroceder e retomar rapidamente. |
| List`< Float>` getAvailablePlaybackRates() | Fornece a lista de taxas de reprodução disponíveis no contexto do recurso de trick-play. |
| Flutuar getSeletedPlaybackRate() | Recupera a taxa de reprodução selecionada no momento. |
| MediaPlayerItemConfig getConfig() | Retorna a instância MediaPlayerItemConfig associada a este item. |
| **Recurso de mídia** |  |
| MediaResource getResource(); | Retorna o recurso de mídia associado a este item. |
| int getResourceId() | Retorna o identificador de mídia associado a este item. Essa ID é definida quando o item é carregado com MediaPlayerItemLoader.load . |