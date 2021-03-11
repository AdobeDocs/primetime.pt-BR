---
description: A lista de reprodução de um vídeo pode especificar um número ilimitado de faixas de áudio alternativas para o conteúdo do vídeo principal. Por exemplo, você pode adicionar idiomas diferentes ao seu conteúdo de vídeo ou permitir que o usuário alterne entre trilhas diferentes em seu dispositivo enquanto o conteúdo está sendo reproduzido.
title: Trilhas de áudio alternativas na lista de reprodução
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Trilhas de áudio alternativas na lista de reprodução {#alternate-audio-tracks-in-the-playlist}

A lista de reprodução de um vídeo pode especificar um número ilimitado de faixas de áudio alternativas para o conteúdo do vídeo principal. Por exemplo, você pode adicionar idiomas diferentes ao seu conteúdo de vídeo ou permitir que o usuário alterne entre trilhas diferentes em seu dispositivo enquanto o conteúdo está sendo reproduzido.

As faixas de áudio alternativas permitem que os usuários alternem entre várias faixas de idioma para fluxos de vídeo HTTP (ao vivo/linear e VOD) e você não precisa modificar, duplicar ou reempacotar o vídeo para cada faixa de áudio. Você pode fornecer várias faixas de idioma para um ativo de vídeo antes ou depois da embalagem inicial do ativo.

>[!IMPORTANT]
>
>Para que o áudio alternativo seja misturado com a faixa de vídeo da mídia principal, os carimbos de data e hora da faixa alternativa devem corresponder aos carimbos de data e hora do áudio na faixa principal.

A faixa de áudio principal está incluída na coleção de faixas de áudio com o rótulo `default`. Os metadados para os fluxos de áudio alternativos estão incluídos na lista de reprodução nas tags `#EXT-X-MEDIA` com `TYPE=AUDIO`.

Por exemplo, um manifesto M3U8 que especifica vários fluxos de áudio alternativos pode ser semelhante a:

```
#EXTM3U
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 1",
 AUTOSELECT=YES,DEFAULT=YES
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 2",
 AUTOSELECT=NO,DEFAULT=NO,URI="alternate_audio_aac/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="eng",URI="subtitles/eng/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English (Forced)",DEFAULT=YES,
 AUTOSELECT=YES,FORCED=YES,LANGUAGE="eng",URI="subtitles/eng_forced/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="Français",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="fra",URI="subtitles/fra/prog_index.m3u8"
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=263851,CODECS="mp4a.40.2, avc1.4d400d",
 RESOLUTION=416x234,AUDIO="bipbop_audio",SUBTITLES="subs" 
gear1/prog_index.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=577610,CODECS="mp4a.40.2, avc1.4d401e",
 RESOLUTION=640x360,AUDIO="bipbop_audio",SUBTITLES="subs"
gear2/prog_index.m3u8
...
```
