---
description: O TVSDK tem requisitos específicos para conteúdo de mídia, conteúdo manifesto, DRM e versões de software.
seo-description: O TVSDK tem requisitos específicos para conteúdo de mídia, conteúdo manifesto, DRM e versões de software.
seo-title: Requisitos
title: Requisitos
uuid: 06e61b9f-cda2-4813-8da4-fb3e0d88ad35
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Requisitos {#requirements}

O TVSDK requer propriedades específicas para conteúdo de mídia, conteúdo manifesto, DRM e versões de software.

## Requisitos de sistema e software {#section_96E5B079900246E78682AE44D3F23068}

Para usar o TVSDK, verifique se as versões de hardware, sistema operacional e aplicativo atendem aos requisitos mínimos listados abaixo.

| Sistema operacional | iOS 7.0 ou posterior |
|---|---|
| Xcode | Xcode 10 para iOS 12 e Xcode 9 para iOS 11 |

## Requisitos de conteúdo e manifesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Verifique as restrições e os requisitos para streams e playlists (manifestos), incluindo chaves de criptografia DRM.

| Quadros principais do segmento de conteúdo | Cada segmento de conteúdo deve começar com um quadro principal. |
|---|---|
| Números de sequência em vídeo ao vivo/linear | Deve corresponder entre todas as execuções de taxa de bits do conteúdo principal em qualquer momento. |

## Requisitos EXT-X-VERSION {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

A versão de `#EXT-X-VERSION` no arquivo manifest [!DNL .m3u8] afeta os recursos disponíveis para seu aplicativo e quais tags `EXT` são válidas.

Estas são algumas informações sobre a tag `#EXT-X-VERSION`, que especifica a versão do protocolo HLS:

* A versão deve corresponder aos recursos e atributos da lista de reprodução HLS; caso contrário, podem ocorrer erros de reprodução. Para obter mais informações, consulte [Especificação HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* O Adobe recomenda usar pelo menos a versão 2 do HLS para reprodução em clientes baseados em TVSDK.

   Os clientes e servidores devem implementar as versões da seguinte maneira:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Usar pelo menos esta versão </th> 
   <th colname="2" class="entry"> Para usar esses recursos </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:2  </span> </td> 
   <td colname="2"> O atributo IV da tag <span class="codeph"> EXT-X-KEY </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duração de <span class="codeph"> EXTINF </span> de ponto flutuante <p>As tags de duração ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) na versão 2 foram arredondados para valores inteiros. A versão 3 e superior exigem que as durações sejam especificadas exatamente, em ponto flutuante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">A tag <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">A tag <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">A tag <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">A tag <span class="codeph"> EXT-X-MEDIA </span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Os atributos <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> da tag <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">Áudio alternativo TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>