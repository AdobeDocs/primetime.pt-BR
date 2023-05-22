---
description: Para inserção de anúncios em streaming ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios do break sejam reproduzidos até a conclusão.
title: Implementar um retorno de ad break antecipado
exl-id: 584e870e-1408-41a9-bb6f-e82b921fe99e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Implementar um retorno de ad break antecipado{#implementing-an-early-ad-break-return}

Para inserção de anúncios em streaming ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios do break sejam reproduzidos até a conclusão.

>[!NOTE]
>
>Você deve assinar os marcadores de anúncio de divisão externa/interna ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, e `#EXT-X-CUE`).

Estes são alguns requisitos a serem considerados:

* Analisar marcadores como `EXT-X-CUE-IN` (ou tag de marcador equivalente) que aparecem nos fluxos linear ou FER.

   Registre os marcadores como sendo o marcador do ponto de retorno antecipado do anúncio. Somente reproduzir `adBreaks` até essa posição do marcador durante a reprodução, que substitui a duração da `adBreak` marcado pela entrelinha `EXE-X-CUE-OUT` marcador.

* Se dois `EXT-X-CUE-IN` existem marcadores para o mesmo `EXT-X-CUE-OUT` marcador, o primeiro `EXT-X-CUE-IN` o marcador exibido é o que conta.

* Se a variável `EXE-X-CUE-IN` marcador aparece na linha do tempo sem uma entrelinha `EXT-X-CUE-OUT` marcador, o `EXE-X-CUE-IN` O marcador é descartado.

   Em um stream ao vivo, se o lead `EXT-X-CUE-OUT` O marcador acabou de ser movido para fora da janela, o TVSDK não responderá a ele.

* Quando houver um retorno antecipado de um ad break, a variável `adBreak` é reproduzido até que o indicador de reprodução retorne à posição original, quando o ad break deveria terminar, e reinicia a reprodução do conteúdo principal dessa posição.

## SpliceOut e SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` e `SpliceIn` marcadores marcam o início e o fim do ad break. A duração do `SpliceOut` tipo de `EXE-X-CUE` o marcador pode ser zero e o `SpliceIn` tipo de `EXE-X-CUE` marca o fim do ad break. Eles aparecem em uma tag e diferem por tipo.

**Um marcador com tipos diferentes**

Por exemplo, aqui está um marcador com tipos diferentes:

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

No exemplo de um marcador com tipos diferentes, se a duração do `SpliceOut` tipo for zero, a variável `SpliceOut` e `SpliceIn` O deve funcionar em conjunto para cada ad break. Atualmente, uma `SpliceOut` marcador com duração diferente de zero e não precisa de emparelhamento `SpliceIn` marcadores é mais típico.

**Dois marcadores separados**

O cenário mais típico é um `SpliceOut` marcador com duração diferente de zero e que não precisa do emparelhamento `SpliceIn` marcadores. Aqui, um par `SpliceIn` marca o fim do ad break durante a reprodução do ad break, mas o ad break está cortado no início `SpliceIn` posição do marcador e o conteúdo principal começa a ser reproduzido nessa posição.

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
