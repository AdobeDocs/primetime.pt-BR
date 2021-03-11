---
description: O áudio alternativo permite que você alterne entre as trilhas de áudio disponíveis para uma faixa de vídeo. Os usuários podem selecionar o rastreamento de idioma preferido quando o vídeo for reproduzido.
title: Áudio alternativo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Visão geral {#alternate-audio-overview}

O áudio alternativo permite que você alterne entre as trilhas de áudio disponíveis para uma faixa de vídeo. Os usuários podem selecionar o rastreamento de idioma preferido quando o vídeo for reproduzido.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando o TVSDK cria a instância `MediaPlayerItem` para o vídeo atual, ele cria um item `AudioTrack` para cada faixa de áudio disponível. O item contém uma propriedade `name`, que é uma string que normalmente contém uma descrição reconhecível pelo usuário do idioma dessa faixa. O item também contém informações sobre se esse rastreamento deve ser usado por padrão. Na hora de reproduzir o vídeo, você pode solicitar uma lista de faixas de áudio disponíveis, permitir que o usuário selecione uma faixa e definir o vídeo para reproduzir com a faixa selecionada.

>[!TIP]
>
>Embora seja raro, se uma faixa de áudio adicional se tornar disponível após o TVSDK criar o `MediaPlayerItem`, o TVSDK acionará um evento `MediaPlayerItem.AUDIO_TRACK_UPDATED`.

## Adição de APIs {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

As seguintes APIs foram adicionadas para suportar áudio alternativo:

**`hasAlternateAudio`**

Se a mídia especificada tiver uma faixa de áudio alternativa, diferente do rastreamento padrão, essa função booleana retornará `true`. Se não houver uma faixa de áudio alternativa, a função retornará `false`.

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

Essa função retorna a lista de todas as faixas de áudio disponíveis em uma mídia especificada.

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

Essa função retorna a faixa de áudio alternativa selecionada no momento e as propriedades, como idioma. A seleção automática da faixa também pode ser extraída.

```java
AudioTrack getSelectedAudioTrack();
```

**`selectAudioTrack`**

Essa função seleciona uma faixa de áudio alternativa para reproduzir.

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
