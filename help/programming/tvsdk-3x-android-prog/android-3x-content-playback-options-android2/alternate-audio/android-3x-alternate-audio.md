---
description: O áudio alternativo permite alternar entre faixas de áudio disponíveis para uma faixa de vídeo. Os usuários podem selecionar sua faixa de idioma preferencial quando o vídeo é reproduzido.
title: Áudio alternativo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Visão geral {#alternate-audio-overview}

O áudio alternativo permite alternar entre faixas de áudio disponíveis para uma faixa de vídeo. Os usuários podem selecionar sua faixa de idioma preferencial quando o vídeo é reproduzido.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando o TVSDK cria a variável `MediaPlayerItem` para o vídeo atual, ele cria uma `AudioTrack` para cada faixa de áudio disponível. O item contém um `name` propriedade, que é uma string que normalmente contém uma descrição reconhecível pelo usuário do idioma dessa faixa. O item também contém informações sobre o uso ou não dessa faixa por padrão. Quando for a hora de reproduzir o vídeo, você pode solicitar uma lista de faixas de áudio disponíveis, permitir opcionalmente que o usuário selecione uma faixa e definir o vídeo para ser reproduzido com a faixa selecionada.

>[!TIP]
>
>Embora seja raro, se uma faixa de áudio adicional ficar disponível após o TVSDK criar a `MediaPlayerItem`, o TVSDK aciona um `MediaPlayerItem.AUDIO_TRACK_UPDATED` evento.

## APIs adicionadas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

As seguintes APIs foram adicionadas para oferecer suporte a áudio alternativo:

**`hasAlternateAudio`**

Se a mídia especificada tiver uma faixa de áudio alternativa, diferente da faixa padrão, essa função booleana retornará `true`. Se não houver faixa de áudio alternativa, a função retornará `false`.

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

Esta função retorna a lista de todas as faixas de áudio disponíveis atualmente em uma mídia especificada.

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

Esta função retorna a faixa de áudio alternativa atualmente selecionada e as propriedades, como idioma. A seleção automática de faixa também pode ser extraída.

```java
AudioTrack getSelectedAudioTrack();
```

**`selectAudioTrack`**

Esta função seleciona uma faixa de áudio alternativa para reproduzir.

```java
void selectAudioTrack(AudioTrack audioTrack);
```

Por exemplo:

```java
private void onPrepared() { 
    // Select the AA track in PREPARED State 
    boolean hasAlternateAudio = _mediaPlayer.getCurrentItem().hasAlternateAudio(); 
    if(hasAlternateAudio) { 
        AudioTrack selectedAudioTrack =  
          _mediaPlayer.getCurrentItem().getSelectedAudioTrack(); 
 
        if (selectedAudioTrack == null) {  
            // Selecting default audio track  
            // If index is 1 it will select alternate audio track  
            selectedAudioTrack = _mediaPlayer.getCurrentItem().getAudioTracks().get(0);  
        } 
    } 
    _mediaPlayer.getCurrentItem().selectAudioTrack(selectedAudioTrack); 
} 
```
