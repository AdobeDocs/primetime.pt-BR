---
description: O TVSDK atualmente fornece suporte de metadados do provedor de anúncios integrado para anúncios TVSDK, quebras de anúncios diretos e marcadores de anúncios personalizados.
seo-description: O TVSDK atualmente fornece suporte de metadados do provedor de anúncios integrado para anúncios TVSDK, quebras de anúncios diretos e marcadores de anúncios personalizados.
seo-title: Tipos de inserção de anúncio
title: Tipos de inserção de anúncio
uuid: 6b5c3555-1ddd-4215-8bb2-03d16bb818c5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Tipos de inserção de anúncio {#ad-insertion-types}

O TVSDK atualmente fornece suporte de metadados do provedor de anúncios integrado para anúncios TVSDK, quebras de anúncios diretos e marcadores de anúncios personalizados.

Ele suporta os seguintes tipos de workflows de inserção de anúncio para conteúdo VOD e live/linear.

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Tipo de inserção </th> 
   <th colname="col2" class="entry"> Suportado em... </th> 
   <th colname="col3" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Anúncios de decisão de anúncios da Adobe Primetime </td> 
   <td colname="col2">VOD <p>Live </p> <p>Linear </p> </td> 
   <td colname="col3">A implementação de referência fornece <span class="codeph"> informações do AuditudeMetadata</span> para conectar-se ao servidor para decisão de anúncio Primetime (anteriormente conhecido como Auditude), com base nas informações fornecidas na parte dos anúncios Primetime</a> do arquivo de configuração JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Quebras de anúncios diretos </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Você deve fornecer URLs de publicidade no arquivo JSON de entrada. Quando o TVSDK tenta resolver um anúncio, ele chama o resolvedor de quebra de anúncio direto e resolve os anúncios com base nas informações de quebra de anúncio direto fornecidas no arquivo de configuração JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marcadores de anúncio personalizados </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Os marcadores de anúncio personalizados são úteis quando o fluxo de vídeo contém conteúdo principal e anúncios, mas não inclui informações relacionadas às posições e ao tempo do anúncio. Se as informações de posicionamento do anúncio forem obtidas de outra forma, por exemplo, por meio de um CMS externo, você poderá definir marcadores de anúncio personalizados e passá-los para a linha do tempo do player. <p>Para configurar um player para inserção de anúncio, é necessário passar os metadados de anúncio na seção de metadados de anúncio personalizados do arquivo de configuração JSON</a>, que tem uma implementação de provedor de anúncio de suporte na implementação de referência. </p> </td>
  </tr>
 </tbody>
</table>