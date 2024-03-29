---
description: O TVSDK requer propriedades específicas para mídia conteúdo, conteúdo de manifesto e versões de software.
title: Requisitos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Requisitos {#requirements}

O TVSDK requer propriedades específicas para conteúdo de mídia, conteúdo de manifesto e versões de software.

## Requisitos de sistema e software {#section_61C32A0209C44230B392B113B85643EE}

Para usar o TVSDK, verifique se o hardware, o sistema operacional e as versões aplicativo atendem aos requisitos mínimos listados abaixo.

Sistema operacional: iOS 6.0 ou posterior

## Requisitos de conteúdo e manifesto {#section_05FA02E2189742008DA09D87E66DCAB7}

Verifique as restrições e requisitos de fluxos e listas de reprodução (manifestos), incluindo chaves de criptografia DRM.

| Conteúdo segmento quadros principais | Cada conteúdo segmento deve começar com um quadro chave. |
|---|---|
| Números de sequência em vídeo ao vivo/linear | Deve corresponder a todas as representações de taxa de bits do conteúdo principal em um determinado momento. |

## Requisitos de #EXT-X-VERSION {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

A versão de `#EXT-X-VERSION` no [!DNL .m3u8] arquivo afeta quais recursos estão disponíveis para o seu aplicativo e quais `EXT` as tags são válidas na lista de reprodução/manifesto.

Estas são algumas informações sobre o `#EXT-X-VERSION` tag, que especifica a versão do protocolo HLS:

* A versão deve corresponder aos recursos e atributos na lista de reprodução do HLS; caso contrário, podem ocorrer erros de reprodução.

  Para obter mais informações, consulte a [especificação](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) HTTP Live Streaming.
* Se a tag não estiver incluída nas listas de reprodução principal ou mídia ou se nenhuma versão for especificada, a versão 1 será usada por padrão. O conteúdo que não está em conformidade com a versão 1 não será reproduzido.
* Adobe Systems recomenda usar pelo menos a versão 2 para reprodução em clientes com base em TVSDK.

Clientes e servidores devem implementar as versões da seguinte maneira:

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> Usar pelo menos esta versão </th> 
   <th colname="2" class="entry"> Para usar esses recursos </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> O atributo IV do <span class="codeph"> EXT-X-KEY </span> tag. </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duração EXTINF </span> de ponto <span class="codeph"> flutuante <p>As tags de duração ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) na versão 2 eram arredondadas para valores inteiros. &lt;/title&gt;&lt;/duration&gt; Versão 3 ou superior requerem durações para serem exatas no ponto flutuante. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> Recursos do TVSDK, como publicidade inserção e ABR perfeita </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> VERSÃO EXT-X:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927">O <span class="codeph"> tag EXT-X-BYTERANGE </span> </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF">O <span class="codeph"> tag EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">A variável <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> tag </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">A variável <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">A variável <span class="codeph"> ÁUDIO </span> e <span class="codeph"> VÍDEO </span> atributos de <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> Áudio alternativo de TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
