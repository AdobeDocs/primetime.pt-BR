---
description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
title: Métodos MediaPlayerItem para acessar informações de MediaResource
exl-id: d6a547f3-0267-4a49-93a4-628b4879aef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Métodos MediaPlayerItem para acessar informações de MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.

| Método | Descrição |
|--- |--- |
| **Tags de publicidade** |  |
| Lista`<String>` getAdTags() | Fornece a lista de tags de anúncio usadas para o processo de posicionamento do anúncio. |
| **Transmissão ao vivo** |  |
| isLive() booleano; | True se o fluxo estiver ativo; false se for VOD. |
| **DRM protegido** |  |
| booleano isProtected(); | True se o fluxo estiver protegido por DRM. |
| Lista`<DRMMetadataInfo>` getDRMMetadataInfos(); | Lista todos os objetos de metadados DRM descobertos no manifesto. |
| **Legendas ocultas** |  |
| booleano hasClosedCaptions(); | Verdadeiro se as faixas de legendas ocultas estiverem disponíveis. |
| Lista`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Fornece uma lista de faixas de legendas ocultas disponíveis. |
| ClosedCaptionsTrack obtém SeletedClosedCaptionsTrack(); | Recupera a faixa atual de legendas ocultas selecionada com SelectClosedCaptionsTrack. |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | Define uma faixa de legendas ocultas para ser a faixa de legendas ocultas atual. |
| **Faixas de áudio alternativas** |  |
| booleano hasAlternateAudio(); | Verdadeiro se o fluxo tiver faixas de áudio alternativas. Observação: a faixa de áudio principal (padrão) também faz parte da lista de faixas de áudio alternativas.  O TVSDK para Android considera a faixa de áudio principal um dos itens na lista de faixas de áudio alternativas. Por causa disso, o único caso em que MediaPlayerItem.hasAlternateAudio retorna falso é quando o fluxo não tem áudio. Se o conteúdo tiver apenas uma faixa de áudio, esse método retornará true e  `MediaPlayerItem.getAudioTracks`  retorna uma lista com um único elemento (a faixa de áudio padrão). |
| Lista`<AudioTrack>` getAudioTracks(); | Fornece uma lista de faixas de áudio alternativas disponíveis. |
| AudioTrack getSelectedAudioTrack(); | Recupera a faixa de áudio selecionada com selectAudioTrack. |
| selectAudioTrack ( AudioTrack audioTrack ) | Seleciona uma faixa de áudio para ser a faixa atual. |
| **Metadados cronometrados** |  |
| booleano hasTimedMetadata(); | True se o fluxo tiver metadados cronometrados associados. |
| Lista`<TimedMetadata>` getTimedMetadata(); | Fornece uma lista dos objetos de metadados cronometrados associados ao fluxo. |
| **Vários perfis (taxas de bits)** |
| isDynamic(); booleano | True se o fluxo for um fluxo de taxa de múltiplos bits (MBR). |
| Lista`<Profile>` getProfiles(); | Fornece uma lista dos perfis de taxa de bits associados. Para cada perfil, você pode recuperar sua taxa de bits e a altura e largura do perfil. |
| Perfil getSelectedProfile() | Recupera o perfil selecionado no momento. |
| **Truque** |  |
| isTrickPlaySupported(); booleano | True se o reprodutor oferecer suporte para avanço rápido, retrocesso e retomada. |
| Lista`< Float>` getAvailablePlaybackRates() | Fornece a lista de taxas de reprodução disponíveis no contexto do recurso de truque. |
| Flutuar getSelectedPlaybackRate() | Recupera a taxa de reprodução selecionada no momento. |
| MediaPlayerItemConfig getConfig() | Retorna a ocorrência de MediaPlayerItemConfig associada a este item. |
| **Recurso de mídia** |  |
| MediaResource getResource(); | Retorna o recurso de mídia associado a este item. |
| int getResourceId() | Retorna o identificador de mídia associado a este item. Essa ID é definida quando o item é carregado usando MediaPlayerItemLoader.load. |
