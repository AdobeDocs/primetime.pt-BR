---
description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
seo-description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
seo-title: Métodos MediaPlayerItem para acessar informações de MediaResource
title: Métodos MediaPlayerItem para acessar informações de MediaResource
uuid: 46845583-0a76-4411-a8bc-0a16ebfe8e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Métodos MediaPlayerItem para acessar informações de MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.

| Método | Descrição |
|--- |--- |
| **Tags de anúncio** |  |
| List`<String>` getAdTags() | Fornece a lista de tags de publicidade usadas no processo de posicionamento do anúncio. |
| **Fluxo ao vivo** |  |
| boolean isLive(); | True se o fluxo for ao vivo; false se for VOD. |
| **DRM protegido** |  |
| boolean isProtected(); | True se o fluxo estiver protegido por DRM. |
| List`<DRMMetadataInfo>` getDRMMetadataInfos(); | Lista todos os objetos de metadados DRM detectados no manifesto. |
| **Legendas ocultas** |  |
| boolean hasClosedCaptions(); | True se as faixas de legenda fechada estiverem disponíveis. |
| List`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Fornece uma lista de faixas de legenda fechada disponíveis. |
| ClosedCaptionsTrack get SeletedCaptionsTrack(); | Recupera o rastreamento de legenda fechada atual selecionado com SelectClosedCaptionsTrack. |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | Define uma faixa de legenda fechada para ser a faixa de legenda fechada atual. |
| **Faixas de áudio alternativas** |  |
| booleano hasAlternateAudio(); | True se o fluxo tiver faixas de áudio alternativas. Observação:  A faixa de áudio principal (padrão) também faz parte da lista de faixa de áudio alternativa.  O TVSDK para Android considera que a faixa de áudio principal é um dos itens na lista de faixa de áudio alternativa. Por esse motivo, o único caso em que MediaPlayerItem.hasAlternateAudio retorna false é quando o fluxo não tem nenhum áudio. Se o conteúdo tiver apenas uma faixa de áudio, esse método retornará true e `MediaPlayerItem.getAudioTracks` retornará uma lista com um único elemento (a faixa de áudio padrão). |
| List`<AudioTrack>` getAudioTracks(); | Fornece uma lista de faixas de áudio alternativas disponíveis. |
| AudioTrack getSeletedAudioTrack(); | Recupera a faixa de áudio selecionada com selectAudioTrack . |
| selectAudioTrack ( AudioTrack audioTrack ) | Seleciona uma faixa de áudio para ser a faixa de áudio atual. |
| **Metadados cronometrados** |  |
| boolean hasTimedMetadata(); | True se o fluxo tiver metadados cronometrados associados. |
| List`<TimedMetadata>` getTimedMetadata(); | Fornece uma lista dos objetos de metadados cronometrados associados ao fluxo. |
| **Vários perfis (taxas de bits)** |
| boolean isDynamic(); | True se o fluxo for um fluxo de taxa de bits múltipla (MBR). |
| List`<Profile>` getProfiles(); | Fornece uma lista dos perfis de taxa de bits associados. Para cada perfil, é possível recuperar sua taxa de bits e a altura e a largura do perfil. |
| Perfil getSeletedProfile() | Recupera o perfil selecionado no momento. |
| **peça** |  |
| boolean isTrickPlaySupported(); | Verdadeiro se o player suportar avanço rápido, retrocesso e retomada. |
| List`< Float>` getAvailablePlaybackRates() | Fornece a lista de taxas de reprodução disponíveis no contexto do recurso de reprodução de truques. |
| Flutuar getSeletedPlaybackRate() | Recupera a taxa de reprodução atualmente selecionada. |
| MediaPlayerItemConfig getConfig() | Retorna a instância MediaPlayerItemConfig associada a este item. |
| **Recurso de mídia** |  |
| MediaResource getResource(); | Retorna o recurso de mídia associado a este item. |
| int getResourceId() | Retorna o identificador de mídia associado a este item. Essa ID é definida quando o item é carregado usando MediaPlayerItemLoader.load. |