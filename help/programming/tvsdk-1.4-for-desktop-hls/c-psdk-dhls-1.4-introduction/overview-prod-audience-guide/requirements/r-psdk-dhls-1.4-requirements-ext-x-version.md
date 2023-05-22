---
description: A versão de EXT-X-VERSION no arquivo .m3u8 afeta quais recursos estão disponíveis para o seu aplicativo e quais tags EXT são válidas na sua lista de reprodução/manifesto.
title: Requisitos do EXT-X-VERSION
exl-id: ee778fe1-d050-4c90-af8d-6600fff72e52
source-git-commit: e2a796dc5eb017929297d127cc79b65ba51a0c75
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Requisitos do EXT-X-VERSION{#ext-x-version-requirements}

A versão de #EXT-X-VERSION no arquivo .m3u8 afeta quais recursos estão disponíveis para seu aplicativo e quais tags EXT são válidas em sua lista de reprodução/manifesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Estas são algumas informações sobre a tag `#EXT-X-VERSION`, que especifica a versão do protocolo HLS:

* A versão deve corresponder aos recursos e atributos na lista de reprodução HLS; caso contrário, erros de reprodução podem ocorrer.

   Para obter mais informações, consulte [Especificação de HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* A versão deve corresponder aos recursos e atributos na lista de reprodução HLS; caso contrário, erros de reprodução podem ocorrer.

   Para obter mais informações, consulte [Especificação de HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* O Adobe recomenda usar pelo menos a versão 2 para reprodução em clientes baseados em.

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> O atributo IV da marca </span> EXT-X-KEY <span class="codeph">. </span></td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores duration <span class="codeph"> EXTINF </span> de ponto flutuante <p>As tags de duração ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) na versão 2 foram arredondadas para valores inteiros. A versão 3 e superior exigem que as durações sejam exatas em ponto flutuante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">A marca </span> EXT-X-BYTERANGE <span class="codeph"> </span></li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">A tag </span> EXT-X-I-FRAME-STREAM-INF do <span class="codeph"> </span></li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">A marca </span> EXT-X-I-FRAMES-ONLY do <span class="codeph"> </span></li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB">A tag </span> DA EXT-X-MEDIA do <span class="codeph"> </span></li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">A variável <span class="codeph"> ÁUDIO </span> e <span class="codeph"> VÍDEO </span> atributos de <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK alternate audio </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
