---
description: O TVSDK tem requisitos específicos para mídia conteúdo, conteúdo de manifesto, DRM e versões de software.
title: Requisitos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Requisitos {#requirements}

O TVSDK tem requisitos específicos para mídia conteúdo, conteúdo de manifesto, DRM e versões de software.

## Requisitos de sistema e software {#section_96E5B079900246E78682AE44D3F23068}

Para usar o TVSDK, verifique se o hardware, o sistema operacional e as versões do aplicativo atendem aos requisitos mínimos listados abaixo.

| Sistema operacional | Android 4.0 ou posterior (nível mínimo de API 14) |
|---|---|
| CPU | 1 GHz Single Core ou equivalente |
| RAM | 256 MB |
| GPU | GPU de hardware necessária para reprodução |
| Arquitetura | x86 via Houdini, ARM64, ARMv7 e ARMv8 |

## Requisitos de conteúdo e manifesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Verifique as restrições e os requisitos para fluxos e listas de reprodução (manifestos), incluindo chaves de criptografia DRM.

| DRM de Acesso ao Adobe | Se o fluxo protegido por DRM for MBR (multiple bit rate), a chave de criptografia DRM usada para o MBR deve ser a mesma que a chave usada em todos os fluxos de taxa de bits. |
|---|---|
| Manifestos de variante de anúncio | Deve ter as mesmas representações de taxa de bits que as representações da conteúdo principal. |

## Requisitos da versão #EXT-X {#section_49A33664651A46EC9ED888BA9C1C3F6D}

A versão do `#EXT-X-VERSION` [!DNL .m3u8] arquivo manifest afeta quais recursos estão disponíveis para sua aplicativo e quais `EXT` tags são válidas.

Estas são algumas informações sobre o `#EXT-X-VERSION` tag, que especifica a versão do protocolo HLS:

* A versão deve corresponder aos recursos e atributos na lista de reprodução do HLS; caso contrário, podem ocorrer erros de reprodução. Para obter mais informações, consulte [Especificação de transmissão HTTP em tempo real](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* A Adobe recomenda usar pelo menos a Versão 2 do HLS para reprodução em clientes baseados em TVSDK.

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
   <td colname="2"> O atributo IV do <span class="codeph"> EXT-X-KEY </span> tag. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duração EXTINF </span> de ponto <span class="codeph"> flutuante <p>As tags de duração ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) na versão 2 eram arredondadas para valores inteiros. &lt;/title&gt;&lt;/duration&gt; Versão 3 e superior requerem durações precisas para serem especificadas exatamente, no ponto flutuante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> VERSÃO EXT-X:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">A variável <span class="codeph"> EXT-X-BYTERANGE </span> tag </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">A variável <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> tag </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">A variável <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> tag </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">A variável <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">A variável <span class="codeph"> ÁUDIO </span> e <span class="codeph"> VÍDEO </span> atributos de <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">Áudio alternativo de TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
