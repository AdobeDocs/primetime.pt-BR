---
description: 'A versão de #EXT-X-VERSION no arquivo .m3u8 afeta os recursos disponíveis para seu aplicativo e quais tags EXT são válidas na lista de reprodução/manifesto.'
seo-description: 'A versão de #EXT-X-VERSION no arquivo .m3u8 afeta os recursos disponíveis para seu aplicativo e quais tags EXT são válidas na lista de reprodução/manifesto.'
seo-title: '#EXT-X-VERSION requirements'
title: '#EXT-X-VERSION requirements'
uuid: 8d22930f-4faf-4a40-b1f0-507886cd8938
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# #EXT-X-VERSION requirements{#ext-x-version-requirements}

A versão de #EXT-X-VERSION no arquivo .m3u8 afeta os recursos disponíveis para seu aplicativo e quais tags EXT são válidas na lista de reprodução/manifesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Estas são algumas informações sobre a tag `#EXT-X-VERSION`, que especifica a versão do protocolo HLS:

* A versão deve corresponder aos recursos e atributos da lista de reprodução HLS; caso contrário, podem ocorrer erros de reprodução. Para obter mais informações, consulte [Especificação HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* O Adobe recomenda usar pelo menos a versão 2 para reprodução em clientes baseados em TVSDK do navegador.

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
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duração de <span class="codeph"> EXTINF </span> de ponto flutuante <p>As tags de duração ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) na versão 2 foram arredondados para valores inteiros. A versão 3 e superior exigem durações exatas em ponto flutuante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">A tag <span class="codeph"> EXT-X-MEDIA </span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Os atributos <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> da tag <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

