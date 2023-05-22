---
description: Áudio alternativo ou de associação tardia permite alternar entre as faixas de áudio disponíveis para uma faixa de vídeo. Dessa forma, os usuários podem selecionar uma faixa de idioma quando o vídeo é reproduzido.
title: Faixas de áudio alternativas na lista de reprodução
exl-id: d8d8c122-5837-4f0e-934f-a3d6e1b037c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Faixas de áudio alternativas na lista de reprodução {#section_BC8C1C74A5A24A8CA68C1E7E721EE742}

A lista de reprodução de um vídeo pode especificar um número ilimitado de faixas de áudio alternativas para o conteúdo de vídeo principal. Por exemplo, você pode adicionar diferentes idiomas ao conteúdo de vídeo ou permitir que o usuário alterne entre diferentes faixas em seu dispositivo enquanto o conteúdo está sendo reproduzido.

Trilhas de áudio alternativas, ou áudio de associação tardia, permitem que os usuários alternem entre várias faixas de idioma para fluxos de vídeo HTTP (ao vivo/linear e VOD) e você não precisa modificar, duplicar ou reempacotar o vídeo para cada faixa de áudio. Você pode fornecer várias rastreamentos de idioma para um ativo de vídeo antes ou depois do empacotamento inicial do ativo.

>[!TIP]
>
>Para que o áudio alternativo seja misturado com a faixa de vídeo da mídia principal, os carimbos de data e hora da faixa alternativa devem corresponder aos carimbos de data e hora do áudio na faixa principal.

Os seguintes requisitos se aplicam se você usar faixas de áudio alternativas e incorporar publicidade:

* Se o conteúdo principal tiver faixas de áudio alternativas, os anúncios devem ter pelo menos um fluxo somente de áudio.
* Cada duração de segmento de um fluxo somente de áudio de anúncio deve ser igual à duração do segmento de um fluxo de vídeo de anúncio.

A faixa de áudio principal está incluída na coleção de faixas de áudio com o `default` rótulo. Os metadados para os fluxos de áudio alternativos estão incluídos na lista de reprodução no `#EXT-X-MEDIA` tags com `TYPE=AUDIO`.

Por exemplo, um manifesto M3U8 que especifica vários fluxos de áudio alternativos pode ter a seguinte aparência:

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
