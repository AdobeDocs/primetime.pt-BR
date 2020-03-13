---
description: O áudio alternativo ou tardio permite alternar entre as faixas de áudio disponíveis para uma faixa de vídeo. Dessa forma, os usuários podem selecionar um rastreamento de idioma quando o vídeo for reproduzido.
seo-description: O áudio alternativo ou tardio permite alternar entre as faixas de áudio disponíveis para uma faixa de vídeo. Dessa forma, os usuários podem selecionar um rastreamento de idioma quando o vídeo for reproduzido.
seo-title: Áudio alternativo
title: Áudio alternativo
uuid: 0abd727c-7036-49c5-a4b7-8945711fecc8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Áudio alternativo {#alternate-audio}

O áudio alternativo ou tardio permite alternar entre as faixas de áudio disponíveis para uma faixa de vídeo. Dessa forma, os usuários podem selecionar um rastreamento de idioma quando o vídeo for reproduzido.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando o TVSDK cria a `MediaPlayerItem` instância do vídeo atual, ele cria um `AudioTrack` item para cada faixa de áudio disponível. O item contém uma `name` propriedade, uma string que geralmente contém uma descrição reconhecível pelo usuário do idioma dessa faixa. O item também contém informações sobre como usar essa faixa por padrão.

Quando for a hora de reproduzir o vídeo, você pode solicitar uma lista de faixas de áudio disponíveis, permitir que o usuário escolha uma e definir o vídeo para reproduzir com a faixa selecionada.

Embora raro, se uma faixa de áudio adicional se tornar disponível depois de criar o `MediaPlayerItem`, o TVSDK acionará um `MediaPlayerItem.AUDIO_UPDATED` evento.

## APIs adicionadas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

As seguintes APIs foram adicionadas para suportar áudio alternativo:

`hasAlternateAudio`

Se a mídia especificada tiver uma faixa de áudio alternativa, diferente da faixa padrão, essa função booleana retornará `true`. Se não houver uma faixa de áudio alternativa, a função retornará `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const { 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

Esta função retorna a lista de todas as faixas de áudio disponíveis atuais em uma mídia especificada.

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const { 
if (_audioTracks) { 
    out = _audioTracks; 
    out->addRef(); 
    return kECSuccess; 
    } 
    return kECDataNotAvailable; 
} 
```

`getSelectedAudioTrack`

Essa função que retorna a faixa de áudio alternativa selecionada no momento e as propriedades, como idioma. A seleção automática da faixa também pode ser extraída.

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const { 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

Esta função seleciona uma faixa de áudio alternativa para reproduzir.

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) { 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```

