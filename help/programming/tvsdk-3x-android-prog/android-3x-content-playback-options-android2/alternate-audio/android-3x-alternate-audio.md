---
description: O áudio alternativo permite alternar entre as faixas de áudio disponíveis para uma faixa de vídeo. Os usuários podem selecionar o rastreamento de idioma preferido quando o vídeo for reproduzido.
seo-description: O áudio alternativo permite alternar entre as faixas de áudio disponíveis para uma faixa de vídeo. Os usuários podem selecionar o rastreamento de idioma preferido quando o vídeo for reproduzido.
seo-title: Áudio alternativo
title: Áudio alternativo
uuid: d1af1ea9-2516-4835-baff-3577ad5b705e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Visão geral {#alternate-audio-overview}

O áudio alternativo permite alternar entre as faixas de áudio disponíveis para uma faixa de vídeo. Os usuários podem selecionar o rastreamento de idioma preferido quando o vídeo for reproduzido.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando o TVSDK cria a `MediaPlayerItem` instância do vídeo atual, ele cria um `AudioTrack` item para cada faixa de áudio disponível. O item contém uma `name` propriedade, que é uma string que geralmente contém uma descrição reconhecível pelo usuário do idioma dessa faixa. O item também contém informações sobre como usar essa faixa por padrão. Quando for a hora de reproduzir o vídeo, você pode solicitar uma lista de faixas de áudio disponíveis, permitir que o usuário selecione uma faixa e defina o vídeo para reproduzir com a faixa selecionada.

>[!TIP]
>
>Embora raro, se uma faixa de áudio adicional se tornar disponível depois que o TVSDK criar o `MediaPlayerItem`, o TVSDK acionará um `MediaPlayerItem.AUDIO_TRACK_UPDATED` evento.

## APIs adicionadas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

As seguintes APIs foram adicionadas para suportar áudio alternativo:

**`hasAlternateAudio`**

Se a mídia especificada tiver uma faixa de áudio alternativa, diferente da faixa padrão, essa função booleana retornará `true`. Se não houver uma faixa de áudio alternativa, a função retornará `false`.

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

Esta função retorna a lista de todas as faixas de áudio disponíveis atuais em uma mídia especificada.

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

Essa função que retorna a faixa de áudio alternativa selecionada no momento e as propriedades, como idioma. A seleção automática da faixa também pode ser extraída.

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
