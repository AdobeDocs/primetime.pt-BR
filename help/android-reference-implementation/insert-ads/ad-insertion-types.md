---
description: O TVSDK atualmente oferece suporte incorporado a metadados do provedor de anúncios para anúncios TVSDK, quebras de anúncios diretos e marcadores de anúncios personalizados.
title: Tipos de inserção de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Tipos de inserção de anúncio {#ad-insertion-types}

O TVSDK atualmente oferece suporte incorporado a metadados do provedor de anúncios para anúncios TVSDK, quebras de anúncios diretos e marcadores de anúncios personalizados.

Ele suporta os seguintes tipos de fluxos de trabalho de inserção de anúncio para VOD e conteúdo ativo/linear.

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
   <td colname="col1"> Anúncios de decisão do Adobe Primetime ad </td> 
   <td colname="col2">VOD <p>Ao vivo </p> <p>Linear </p> </td> 
   <td colname="col3">A implementação de referência fornece informações <span class="codeph"> AuditudeMetadata</span> para se conectar ao servidor para decisão de anúncio do Primetime (anteriormente conhecido como Auditude), com base nas informações fornecidas na porção de anúncios do Primetime</a> do arquivo de configuração JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Quebras de anúncios diretos </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Você deve fornecer URLs de publicidade no arquivo JSON de entrada. Quando o TVSDK tenta resolver um anúncio, ele chama o resolvedor de ad break direto e resolve os anúncios com base nas informações de ad break direto fornecidas no arquivo de configuração JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marcadores de anúncio personalizados </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Os marcadores de anúncio personalizados são úteis quando o fluxo de vídeo contém conteúdo principal e anúncios, mas não inclui informações relacionadas às posições e tempo do anúncio. Se as informações de posicionamento do anúncio forem obtidas de outra maneira, por exemplo, por meio de um CMS externo, é possível definir marcadores de anúncio personalizados e transmiti-los para a linha do tempo do player. <p>Para configurar um reprodutor para inserção de anúncio, você precisa transmitir metadados de anúncio na seção Metadados de anúncio personalizados do arquivo de configuração JSON</a>, que tem uma implementação de provedor de anúncio de suporte na implementação de referência. </p> </td>
  </tr>
 </tbody>
</table>