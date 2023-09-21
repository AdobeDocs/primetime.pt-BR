---
description: Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.
title: Classes de publicidade da linha do tempo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Classes de publicidade da linha do tempo{#timeline-advertising-classes}

Essas classes fornecem informações sobre anúncios que ocorrem em uma linha do tempo.

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">Classe que define a abstração do anúncio e contém todas as informações do anúncio. É definida por uma ID exclusiva, uma duração e um MediaResource. O MediaResource contém o URL onde o conteúdo real do anúncio está. 
    <pre>
      Representa um ativo linear principal dividido no conteúdo. Opcionalmente, pode conter uma matriz de ativos complementares que devem ser exibidos junto com o ativo linear.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">Classe que representa um ativo a ser exibido. 
    <pre>
      Representa um ativo a ser exibido.
    </pre> 
    <pre>
      Classe que representa um ativo de anúncio.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      Exibe um ativo de banner. Seu aplicativo deve criar uma nova instância dessa classe de utilitário, definir o ativo de banner e adicioná-lo a uma visualização. O rastreamento de impressões e cliques para o banner é gerenciado internamente por essa classe.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdbreak</a> </td> 
   <td colname="2">Classe que fornece uma visualização unificada de vários anúncios que serão reproduzidos em algum momento durante a reprodução. 
    <pre>
      Representa uma sequência contínua de anúncios divididos no conteúdo.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">Classe que representa uma instância de clique associada a um ativo. Essa instância contém informações sobre o URL de click-through e o título que pode ser usado para fornecer informações adicionais ao usuário. 
    <pre>
      Representa uma instância de clique associada a um ativo. Essa instância contém informações sobre o URL de click-through e o título que pode ser usado para fornecer informações adicionais ao usuário.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> Protocolo que define propriedades para chamadas de API AdPolicySelector. Essas propriedades fornecem o contexto para impor cada comportamento de anúncio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PTAdPolicySelector</td> 
   <td colname="2"> Um protocolo de seletor de políticas de anúncios para impor comportamentos de anúncios. Os aplicativos podem estar em conformidade com esse protocolo implementando todos os métodos necessários ou estendendo a classe do seletor de políticas padrão existente para personalizar comportamentos específicos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> PTAdTimeline</td> 
   <td colname="2"> Classe que representa a linha do tempo de quebras no conteúdo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> classe, 
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> protocolo
    </pre> </td> 
   <td colname="2"> Classe que manipula a parte de resolução de anúncios no processo de decisão de anúncios da Adobe Primetime. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> Protocolo que descreve os métodos do resolvedor de conteúdo personalizado ( <span class="codeph"> PTContentResolver</span> ) deve usar para comunicar ao delegado o status da resolução do conteúdo. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">Classe que abstrai uma solicitação de informações de posicionamento. Cada anúncio resolvido deve ter uma informação de posicionamento anexada a ele. As informações de posicionamento descrevem onde o anúncio deve ser colocado na linha do tempo. Ele contém informações como: 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">Posição do posicionamento (em ms) </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">Tipo de posicionamento (antes da exibição, durante a exibição ou após a exibição) </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">Duração da parte do conteúdo principal que está prestes a ser substituída </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
