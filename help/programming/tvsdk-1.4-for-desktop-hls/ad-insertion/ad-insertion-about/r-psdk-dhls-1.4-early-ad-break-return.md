---
description: Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.
seo-description: Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.
seo-title: Implementação de um retorno antecipado de anúncios
title: Implementação de um retorno antecipado de anúncios
uuid: 984b6ed0-c929-49a3-9553-e30d1a7758ed
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementação de um retorno antecipado de anúncios{#implementing-an-early-ad-break-return}

Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.

>[!NOTE] {othertype=&quot;Pré-requisito&quot;}
>
>Você deve assinar os marcadores de saída/entrada do anúncio ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`e `#EXT-X-CUE`).

Estes são alguns requisitos a serem considerados:

* Analise marcadores como `EXT-X-CUE-IN` (ou tag de marcador equivalente) que aparecem nos fluxos lineares ou FER.

   Registre os marcadores como sendo o marcador do ponto de retorno inicial do anúncio. Reproduzir somente `adBreaks` até que esse marcador posicione durante a reprodução, o que substitui a duração do marcador `adBreak` marcado pelo `EXE-X-CUE-OUT` marcador à esquerda.

* Se existirem dois `EXT-X-CUE-IN` marcadores para o mesmo `EXT-X-CUE-OUT` marcador, o primeiro `EXT-X-CUE-IN` marcador que aparece é o que conta.

* Se o `EXE-X-CUE-IN` marcador aparecer na linha do tempo sem um `EXT-X-CUE-OUT` marcador à esquerda, o `EXE-X-CUE-IN` marcador será descartado.

   Em um fluxo ao vivo, se o `EXT-X-CUE-OUT` marcador à esquerda acaba de sair da janela, o TVSDK não responderá a ele.

* Quando há um retorno antecipado de uma pausa de anúncio, o indicador de reprodução é reproduzido `adBreak` até que retorne à posição original quando o intervalo do anúncio deveria terminar e retome a reprodução do conteúdo principal dessa posição.

## SpliceOut e SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` e os `SpliceIn` marcadores marcam o início e o fim do intervalo do anúncio. A duração do `SpliceOut` tipo do `EXE-X-CUE` marcador pode ser zero e o `SpliceIn` tipo de `EXE-X-CUE` marcador marca o fim da quebra do anúncio. Elas aparecem em uma tag e diferem por tipo.

**Um marcador com tipos diferentes**

Por exemplo, há um marcador com tipos diferentes:

```
#EXTM3U#EXT-X-TARGETDURATION:10
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:44
  
#EXTINF:9.9,
https://server-host/path/file44.ts
#EXTINF:4.2,
https://server-host/path/file45.ts
  
#EXT-X-CUE:TYPE="SpliceOut",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138",AVAIL-NUM="1",AVAILS-EXPECTED="10"
#EXTINF:5.8,
https://server-host/path/file46.ts
#EXTINF:9.9,
https://server-host/path/file47.ts
...
#EXTINF:9.9,
https://server-host/path/file56.ts
#EXTINF:4.2,
https://server-host/path/file57.ts
#EXT-X-CUE:TYPE="SpliceIn",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138"
#EXTINF:9.9,
https://server-host/path/file58.ts
```

No exemplo de um marcador com tipos diferentes, se a duração do `SpliceOut` tipo for zero, o `SpliceOut` e `SpliceIn` deverá trabalhar em conjunto para cada quebra de anúncio. Atualmente, um `SpliceOut` marcador com duração diferente de zero e sem precisar de `SpliceIn` marcadores de emparelhamento é mais típico.

**Dois marcadores separados**

O cenário mais típico é um `SpliceOut` marcador com uma duração diferente de zero e que não precisa dos `SpliceIn` marcadores de emparelhamento. Aqui, um `SpliceIn` marcador de emparelhamento marca o término do intervalo do anúncio durante a reprodução do intervalo, mas o intervalo do anúncio é curto na posição do `SpliceIn` marcador e o conteúdo principal começa a ser reproduzido nessa posição.

Por exemplo, há dois marcadores separados:

```
#EXT-X-CUE-OUT:ID=105,DURATION=30.0,TIME=1081.08
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589090425811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589150485811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589210545811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589270605811,format=m3u8-aapl-v4)
#EXT-X-CUE-IN:ID=105,TIME=1105.104
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589330665811,format=m3u8-aapl-v4)
```

