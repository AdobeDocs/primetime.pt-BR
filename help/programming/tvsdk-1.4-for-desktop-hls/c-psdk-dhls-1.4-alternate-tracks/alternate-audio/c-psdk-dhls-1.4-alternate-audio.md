---
description: Áudio alternativo ou de associação tardia permite alternar entre as faixas de áudio disponíveis para uma faixa de vídeo. Dessa forma, os usuários podem selecionar uma faixa de idioma quando o vídeo é reproduzido.
title: Áudio alternativo
exl-id: 0a40fbd9-f043-4296-9f07-d75bacf793f8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Áudio alternativo{#alternate-audio}

Áudio alternativo ou de associação tardia permite alternar entre as faixas de áudio disponíveis para uma faixa de vídeo. Dessa forma, os usuários podem selecionar uma faixa de idioma quando o vídeo é reproduzido.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando o TVSDK cria a variável `MediaPlayerItem` para o vídeo atual, ele cria uma `AudioTrack` para cada faixa de áudio disponível. O item contém um `name` propriedade, uma string que normalmente contém uma descrição reconhecível pelo usuário do idioma dessa faixa. O item também contém informações sobre o uso ou não dessa faixa por padrão.

Quando for a hora de reproduzir o vídeo, você pode solicitar uma lista de faixas de áudio disponíveis, permitir que o usuário escolha uma e definir o vídeo para ser reproduzido com a faixa selecionada.

Embora seja raro, se uma faixa de áudio adicional ficar disponível após criar a `MediaPlayerItem`, o TVSDK aciona um `MediaPlayerItem.AUDIO_UPDATED` evento.

## APIs adicionadas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

As seguintes APIs foram adicionadas para oferecer suporte a áudio alternativo:

`hasAlternateAudio`

Se a mídia especificada tiver uma faixa de áudio alternativa, diferente da faixa padrão, essa função booleana retornará `true`. Se não houver faixa de áudio alternativa, a função retornará `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const { 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

Esta função retorna a lista de todas as faixas de áudio disponíveis atualmente em uma mídia especificada.

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

Esta função retorna a faixa de áudio alternativa atualmente selecionada e as propriedades, como idioma. A seleção automática de faixa também pode ser extraída.

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
