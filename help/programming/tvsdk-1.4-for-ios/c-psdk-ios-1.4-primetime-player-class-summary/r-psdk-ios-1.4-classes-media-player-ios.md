---
description: Essas classes descrevem o reprodutor de mídia e seus recursos.
title: Classes do reprodutor de mídia
exl-id: de7f7488-2026-43b4-b74d-feff67bdc69a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Classes do reprodutor de mídia {#media-player-classes}

Você pode usar a API Objetive-C do reprodutor Primetime para personalizar o comportamento do reprodutor.

Essas classes descrevem o reprodutor de mídia e seus recursos.

<table frame="all" colsep="1" rowsep="1" id="table_bm2_wl2_2m"> 
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Classe</b> </td> 
   <td colname="2"><b>Descrição</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTABRControlParameters.html" format="html" scope="external"> PTABRControlParameters</a></span> </td> 
   <td colname="2">Encapsula todos os parâmetros de controle de taxa de bits adaptáveis. Os parâmetros compatíveis são: 
    <ul id="ul_pnh_hm2_2m"> 
     <li id="li_46572FE1EB514AFF8C9F731E44DAF30B"><span class="codeph"> minBitRate</span> </li> 
     <li id="li_A10C75C9A5234241A5B84A4139F4D143"><span class="codeph"> maxBitRate</span> </li> 
     <li id="li_4E77E367A2E848D2B3E1A9C52209A7B2"><span class="codeph"> taxaDeBitsInicial</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDefaultMediaPlayerClientFactory.html" format="html" scope="external"> PTDefaultMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> Implementação padrão de <span class="codeph"> PTMediaPlayerClientFactory</span> no TVSDK. Ele fornece os recursos disponíveis <span class="codeph"> PTOpportunityResolver</span>, <span class="codeph"> PTContentResolver</span>, e <span class="codeph"> PTAdPolicySelector</span> instâncias. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html" format="html" scope="external"> PTMediaPlayer</a></span> </td> 
   <td colname="2">Define o componente raiz da estrutura do Primetime Player. <p>Os aplicativos criam uma ocorrência dessa classe para reproduzir uma mídia. Esse componente envia notificações para informar ao aplicativo o status do reprodutor a qualquer momento. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTMediaPlayerClientFactory.html" format="html" scope="external"> PTMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> Protocolo que descreve os métodos que uma fábrica de clientes de reprodutor de mídia personalizado deve implementar para fornecer os <span class="codeph"> PTOpportunityResolver</span> , <span class="codeph"> PTContentResolver</span> e <span class="codeph"> PTAdPolicySelector</span> instâncias. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerItem.html" format="html" scope="external"> PTMediaPlayerItem</a></span> </td> 
   <td colname="2"> Representa uma mídia de áudio e vídeo específica. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerView.html" format="html" scope="external"> ExibiçãoDoPlayerDeMídiaPTM</a></span> </td> 
   <td colname="2"> Gerencia o componente de exibição da estrutura do Primetime Player. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaProfile.html" format="html" scope="external"> PTMediaProfile</a></span> </td> 
   <td colname="2"> Representa o perfil de um único fluxo na lista de reprodução de variantes. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaSelectionOption.html" format="html" scope="external"> PTMediaSelectionOption</a></span> </td> 
   <td colname="2">Representa um recurso de mídia audiovisual para acomodar diferentes preferências de idioma, requisitos de acessibilidade ou configurações de aplicativo personalizadas. Tipos de opção válidos: 
    <ul id="ul_p2q_gn2_2m"> 
     <li id="li_46BE5AE49732481FB6D336FFF896E5AD">Legendas (<span class="codeph"> SubtítuloTipoOpçãoSeleçãoMídiaPTM</span>) </li> 
     <li id="li_6CEADCA12D4A48B7AE4A539985F32119">Áudio alternativo (<span class="codeph"> PTMediaSelectionOptionTypeAudio</span>) </li> 
     <li id="li_248D3D997F8A4B6E9B48869F84060D1F"> <p>Indefinido (<span class="codeph"> PTMediaSelectionOptionTypeUndefined</span>) </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTOpportunityResolver.html" format="html" scope="external"> PTOpportunityResolver</a> </span> classe, <span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolver.html" format="html" scope="external"> PTOpportunityResolver</a> protocolo</span> </td> 
   <td colname="2"> Classe usada para processar indicações no manifesto que serão usadas como disposições para o processo de decisão de anúncios do Adobe Primetime. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolverDelegate.html" format="html" scope="external"> PTOpportunityResolverDelegate</a></span> </td> 
   <td colname="2"> Protocolo que descreve os métodos do resolvedor de oportunidades personalizado ( <span class="codeph"> PTOpportunityResolver</span> ) deve usar para comunicar ao delegado o status da resolução da oportunidade. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDK.html" format="html" scope="external"> PTSDK</a></span> </td> 
   <td colname="2"> Descreve a versão do TVSDK e seus recursos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDKConfig.html" format="html" scope="external"> PTSDKConfig</a></span> </td> 
   <td colname="2"> Expõe as configurações globais do TVSDK e permite que um aplicativo assine tags HLS personalizadas. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTextStyleRule.html" format="html" scope="external"> PTTextStyleRule</a></span> </td> 
   <td colname="2"> Define as constantes que representam as chaves de atributo de estilo de texto que formam o dicionário de regras. </td> 
  </tr> 
 </tbody> 
</table>
