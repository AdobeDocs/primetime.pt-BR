---
description: O TVSDK requer propriedades específicas para conteúdo de mídia, conteúdo manifesto e versões de software.
seo-description: O TVSDK requer propriedades específicas para conteúdo de mídia, conteúdo manifesto e versões de software.
seo-title: Requisitos
title: Requisitos
uuid: 7e5fb176-4c3f-4c12-9080-3afced28627b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Requisitos {#requirements}

O TVSDK requer propriedades específicas para conteúdo de mídia, conteúdo manifesto e versões de software.

## Requisitos de sistema e software {#section_61C32A0209C44230B392B113B85643EE}

Para usar o TVSDK, verifique se as versões de hardware, sistema operacional e aplicativo atendem aos requisitos mínimos listados abaixo.

Sistema operacional: iOS 6.0 ou posterior

## Requisitos de conteúdo e manifesto {#section_05FA02E2189742008DA09D87E66DCAB7}

Verifique as restrições e os requisitos para streams e playlists (manifestos), incluindo chaves de criptografia DRM.

| Quadros principais do segmento de conteúdo | Cada segmento de conteúdo deve começar com um quadro principal. |
|---|---|
| Números de sequência em vídeo ao vivo/linear | Deve corresponder entre todas as execuções de taxa de bits do conteúdo principal em qualquer momento. |

## #EXT-X-VERSION requirements {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

A versão de `#EXT-X-VERSION` no arquivo [!DNL .m3u8] afeta os recursos disponíveis para seu aplicativo e quais tags `EXT` são válidas na lista de reprodução/manifesto.

Estas são algumas informações sobre a tag `#EXT-X-VERSION`, que especifica a versão do protocolo HLS:

* A versão deve corresponder aos recursos e atributos da lista de reprodução HLS; caso contrário, podem ocorrer erros de reprodução.

   Para obter mais informações, consulte [Especificação HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Se a tag não estiver incluída nas listas de reprodução principais ou de mídia, ou se nenhuma versão for especificada, a versão 1 será usada por padrão. O conteúdo que não estiver em conformidade com a versão 1 não será reproduzido.
* O Adobe recomenda usar pelo menos a versão 2 para reprodução em clientes baseados em TVSDK.

Os clientes e servidores devem implementar as versões da seguinte maneira:

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> Usar pelo menos esta versão </th> 
   <th colname="2" class="entry"> Para usar esses recursos </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:2  </span> </td> 
   <td colname="2"> O atributo IV da tag <span class="codeph"> EXT-X-KEY </span>. </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duração de <span class="codeph"> EXTINF </span> de ponto flutuante <p>As tags de duração ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) na versão 2 foram arredondados para valores inteiros. A versão 3 e superior exigem durações exatas em ponto flutuante. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> Recursos do TVSDK, como inserção de anúncios e ABR integrado </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> VERSÃO EXT-X:4  </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927">A tag <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF">A tag <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">A tag <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">A tag <span class="codeph"> EXT-X-MEDIA </span> </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">Os atributos <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> da tag <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> Áudio alternativo TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
