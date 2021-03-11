---
description: Os editores podem criar players de vídeo compatíveis com HLS que funcionam com os fluxos de trabalho de rastreamento de anúncios do lado do cliente do servidor de manifesto do Primetime. As interfaces com o servidor de manifesto para os casos de transmissão ao vivo e vídeo sob demanda (VOD) são um pouco diferentes.
title: Visão geral do rastreamento não TVSDK pelo lado do cliente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---


# Visão geral do rastreamento não TVSDK pelo lado do cliente {#overview-of-non-tvsdk-client-side-tracking}

Os editores podem criar players de vídeo compatíveis com HLS que funcionam com os fluxos de trabalho de rastreamento de anúncios do lado do cliente do servidor de manifesto do Primetime. As interfaces com o servidor de manifesto para os casos de transmissão ao vivo e vídeo sob demanda (VOD) são um pouco diferentes.

O servidor de manifesto fornece uma API para permitir que os players personalizados solicitem os seguintes URLs, que podem ser usados para relatar eventos de rastreamento de anúncios:

* Impressão do anúncio
* Quartil do anúncio
* Progresso do pod de anúncio
* Progresso do pod de conteúdo

A API do servidor de manifesto presume que qualquer player de vídeo que o use atenda aos requisitos mínimos. Consulte [Requisitos do reprodutor de vídeo](/help/primetime-ad-insertion/~old-msapi-topics/ms-player-req.md) para obter mais detalhes.

## Fluxo de trabalho de rastreamento do lado do cliente {#section_cst_flow}

![](assets/pt_ssai_notvsdk_csat_ai-workflow.png)

1. O reprodutor obtém um URL de servidor de manifesto do publicador.
1. O Player anexa parâmetros de consulta específicos aos requisitos de inserção de anúncios e envia uma solicitação HTTP do GET para o URL do Bootstrap resultante. O URL do Bootstrap tem a seguinte sintaxe:

   ```URL
   http{s}://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{urlSafeBase64({Content URL})}.m3u8?{query parameters}
   ```

   Por exemplo:

   ```URL
   https://manifest.auditude.com/auditude/variant/
   7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.m3u8?
   u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2&__sid__=docExample02
   ```

   O URL inclui os elementos descritos em [Send a command to the Manifest Server](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-sending-cmd.md).

1. O servidor de manifesto estabelece uma sessão para esse reprodutor e gera uma ID de sessão exclusiva. Ele cria uma nova variante do URL da lista de reprodução M3U8, que retorna ao reprodutor como uma resposta JSON. O JSON tem a seguinte sintaxe:

   ```JSON
   {
    "Master-M3U8": "https://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{SessionID}/
       {urlSafeBase64(content URL)}.m3u8?u={Asset ID}&z={Zone ID}&pttrackingmode=simple&pttrackingversion=v2
       &{Any other query parameters}"
   }
   ```

   Por exemplo:

   ```JSON
   https://pcor3.manifest.auditude.com/auditude/variant/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. O reprodutor usa o URL da resposta JSON para solicitar a nova lista de reprodução principal M3U8 do servidor de manifesto.

1. O servidor de manifesto retorna uma nova variante M3U8 contendo URLs de lista de reprodução em nível de fluxo com uma sintaxe semelhante à seguinte:

   ```URL
   http{s}://{manifest-server:port}/auditude/{live|vod}/{PublisherAssetID}/
     {rendition}/{groupID}/{urlSafeBase64(bit rate stream URL)}.m3u8?u={Ad Request Id}&z={Ad Zone Id}&{Any other query parameters}
   ```

   Por exemplo:

   ```URL
   #EXTM3U
   #EXT-X-VERSION:5
   #EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,DEFAULT=YES,FORCED=NO,LANGUAGE="eng",URI="https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/webvtt/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvd2VidnR0L1RPUy1lbjIubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2"
   #EXT-X-STREAM-INF:BANDWIDTH=10000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/10000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTAwMDAvdG9jXzEwMDAwLm0zdTg.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=1300000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/1300/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTMwMC90b2NfMTMwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=3400000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/3400/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMzQwMC90b2NfMzQwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=2100000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/2100/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMjEwMC90b2NfMjEwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=800000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/800/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvODAwL3RvY184MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=5000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/5000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwMC90b2NfNTAwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=7500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/7500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNzUwMC90b2NfNzUwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. O reprodutor seleciona a taxa de bits única apropriada, o URL de manifesto em nível de fluxo para reproduzir o conteúdo corrigido do anúncio. Por exemplo:

   ```URL
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. O servidor de manifesto retorna um manifesto de nível de fluxo contendo links para o conteúdo e links de segmento TS de anúncio. Por exemplo:

   ```
      #EXTM3U
   #EXT-X-VERSION:3
   #EXT-X-TARGETDURATION:8
   #EXT-X-PLAYLIST-TYPE:VOD
   
   #EXT-X-DISCONTINUITY
   #EXTINF:8,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00001.ts
   #EXTINF:7,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00002.ts
   
   #EXT-X-DISCONTINUITY
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.0.ts
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.4000.ts
   #EXTINF:4.833,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.8000.ts   
   ```

   >[!NOTE]
   >
   >O reprodutor seleciona o URL da lista de reprodução em nível de fluxo para obter o fluxo de conteúdo. O servidor manifest recupera a lista de reprodução original da CDN. Alguns codificadores podem inserir detalhes adicionais no atributo de título `#EXTINF`, por exemplo:
   >
   >
   ```
   >#EXTINF:6.006,LTC=2017-08-23T13:25:47+00:00
   >```

   Como o servidor de manifesto não pode inferir o significado de atributos não padrão para modificá-los para uma lista de reprodução com costura de anúncio, o servidor de manifesto remove todos os atributos adicionais além das informações de duração nesta tag. Consulte a entrada [EXTINF](https://tools.ietf.org/html/rfc8216#section-4.3.2.1) na especificação do HLS para obter mais detalhes.

1. Para solicitar informações de rastreamento, o reprodutor anexa o parâmetro de consulta `pttrackingposition` com qualquer valor alfanumérico ao URL da lista de reprodução no nível do fluxo para a taxa de bits selecionada. Por exemplo:

   ```URL
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d
   &z=173475&pttrackingmode=simple&pttrackingversion=v2&pttrackingposition=1
   ```

1. O servidor de manifesto retorna o arquivo de lista de reprodução preenchido com um objeto [JSON](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md) ou [VMAP](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md) contendo os dados de rastreamento de anúncio para o arquivo m3u8 de nível de fluxo atualmente solicitado.

   >[!NOTE]
   >
   >O servidor de manifesto só gerará objetos de rastreamento de anúncios se anúncios tiverem sido inseridos na lista de reprodução em nível de fluxo solicitada no momento. Se o reprodutor estiver reproduzindo uma lista de reprodução que não contém anúncios inseridos, o servidor de manifesto retornará um Status HTTP 201 para a solicitação da lista de reprodução de rastreamento de anúncio. Se o reprodutor fizer a solicitação de rastreamento de anúncio para um fluxo que não está sendo reproduzido, o servidor de manifesto retornará um Status HTTP 500. Por exemplo, se a solicitação de reprodução atual for 500.m3u8, o servidor de manifesto retornará um JSON|VMAP no 500.m3u8 para a solicitação de rastreamento de anúncio. No entanto, se o reprodutor alternar fluxos para reproduzir o 800.m3u8 posteriormente, as informações de rastreamento de anúncio no 500.m3u8 se tornarão inválidas, resultando em um erro 404.

   >[!NOTE]
   >
   >O servidor manifest gera o objeto de rastreamento de anúncios com base no valor `pttrackingversion` no URL do Bootstrap. Se `pttrackingversion` for omitido ou tiver um valor inválido, o servidor de manifesto preencherá automaticamente as informações de rastreamento de anúncio nas tags `#EXT-X-MARKER` em cada lista de reprodução de nível de fluxo solicitada. Consulte [para obter mais detalhes](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md).

1. O reprodutor solicita cada URL de rastreamento de anúncio para cada evento de rastreamento de anúncio no momento apropriado.

>[!NOTE]
>
>Para fluxos ao vivo, o reprodutor deve repetir as etapas de 6 a 10, pois o empacotador atualiza constantemente a lista de reprodução durante toda a duração do evento ao vivo.

Conforme o vídeo é reproduzido, o reprodutor deve rastrear a posição do indicador de reprodução e usar essa posição junto com os URLs de rastreamento recebidos do Primetime ad insertion. Os URLs de rastreamento são agrupados por deslocamento de tempo a partir do início da reprodução. Para cada deslocamento de tempo, há um URL para cada sistema de anúncios para o qual enviar informações de rastreamento. Detalhes adicionais do formato diferem entre vídeo ao vivo e vídeo sob demanda.
