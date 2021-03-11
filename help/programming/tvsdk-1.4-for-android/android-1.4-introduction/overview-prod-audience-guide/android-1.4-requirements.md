---
description: O TVSDK requer requisitos específicos para conteúdo de mídia, conteúdo manifesto, DRM e versões de software.
title: Requisitos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Requisitos {#requirements}

O TVSDK requer requisitos específicos para conteúdo de mídia, conteúdo manifesto, DRM e versões de software.

## Requisitos de sistema e software {#section_96E5B079900246E78682AE44D3F23068}

Para usar o TVSDK, verifique se as versões do hardware, do sistema operacional e do aplicativo atendem aos requisitos mínimos listados abaixo.

| Sistema operacional | Android 4.0 ou posterior (nível mínimo de API 14) |
|---|---|
| CPU | 1 GHz Single Core ou equivalente |
| RAM | 256 MB |
| GPU | GPU de hardware necessária para a reprodução |
| Arquitetura | x86 via Houdini, ARM64, ARMv7 e ARMv8 |

## Requisitos de conteúdo e manifesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Verifique as restrições e os requisitos para fluxos e listas de reprodução (manifestos), incluindo chaves de criptografia de DRM.

| DRM de acesso ao Adobe | Se o fluxo protegido por DRM for de taxa múltipla de bits (MBR), a chave de criptografia de DRM usada para o MBR deverá ser a mesma usada em todos os fluxos de taxa de bits. |
|---|---|
| Manifestações de variante de anúncio | Deve ter as mesmas representações de taxa de bits que as representações do conteúdo principal. |

## #EXT-X-VERSION requirements {#section_49A33664651A46EC9ED888BA9C1C3F6D}

A versão de `#EXT-X-VERSION` no arquivo [!DNL .m3u8] afeta quais recursos estão disponíveis para seu aplicativo e quais `EXT` tags são válidas em sua lista de reprodução/manifesto.

Estas são algumas informações sobre a tag `#EXT-X-VERSION` , que especifica a versão do protocolo HLS:

* A versão deve corresponder aos recursos e atributos na lista de reprodução do HLS; caso contrário, podem ocorrer erros de reprodução. Para obter mais informações, consulte a [especificação do HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> O atributo IV da tag <span class="codeph"> EXT-X-KEY </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duração de ponto flutuante <span class="codeph"> EXTINF </span> <p>As marcas de duração ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) na versão 2 foram arredondadas para valores inteiros. A versão 3 e superior exigem que as durações sejam especificadas exatamente, em ponto flutuante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4  </span> </td> 
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

