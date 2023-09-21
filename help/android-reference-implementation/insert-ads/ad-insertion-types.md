---
description: Atualmente, o TVSDK fornece suporte a metadados de provedor de anúncios integrados para anúncios TVSDK, ad breaks diretos e marcadores de anúncios personalizados.
title: Tipos de inserção de anúncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Tipos de inserção de anúncio {#ad-insertion-types}

Atualmente, o TVSDK fornece suporte a metadados de provedor de anúncios integrados para anúncios TVSDK, ad breaks diretos e marcadores de anúncios personalizados.

Ela é compatível com os seguintes tipos de fluxos de trabalho de inserção de anúncios para VOD e conteúdo dinâmico/linear.

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Tipo de inserção </th> 
   <th colname="col2" class="entry"> Compatível com... </th> 
   <th colname="col3" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Anúncios do Adobe Primetime Ad Decisioning </td> 
   <td colname="col2">VOD <p>Ao vivo </p> <p>Linear </p> </td> 
   <td colname="col3">A implementação de referência fornece <span class="codeph"> AuditudeMetadata</span> informações para se conectar ao servidor para o Primetime ad decisioning (anteriormente conhecido como Auditude), com base nas informações fornecidas na parte de anúncios do Primetime</a> do arquivo de configuração JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Intervalos de publicidade diretos </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Você deve fornecer URLs de anúncios no arquivo JSON de entrada. Quando o TVSDK tenta resolver um anúncio, ele chama o resolvedor direto de ad break e resolve os anúncios com base nas informações diretas de ad breaks fornecidas no arquivo de configuração JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marcadores de publicidade personalizados </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Os marcadores de anúncios personalizados são úteis quando o fluxo de vídeo contém conteúdo principal e anúncios, mas não inclui informações relacionadas às posições e ao tempo do anúncio. Se as informações de posicionamento do anúncio forem obtidas de outra maneira, por exemplo, por meio de um CMS externo, será possível definir marcadores de anúncio personalizados e transmiti-los à linha do tempo do reprodutor. <p>Para configurar um reprodutor para inserção de anúncio, é necessário transmitir metadados de anúncio na seção metadados de anúncio personalizados do arquivo de configuração JSON</a>, que tem uma implementação de provedor de anúncios de suporte na implementação de referência. </p> </td>
  </tr>
 </tbody>
</table>
