---
description: Esta tabela mostra informações detalhadas sobre notificações de tipo WARN.
seo-description: Esta tabela mostra informações detalhadas sobre notificações de tipo WARN.
seo-title: Códigos de notificação de AVISO
title: Códigos de notificação de AVISO
uuid: da1a561d-3b9a-468a-a24a-7b6fa62aa2e8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 3%

---


# Códigos de notificação de AVISO {#warning-notification-codes}

Esta tabela mostra informações detalhadas sobre notificações de tipo WARN.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

A maioria dos avisos contém metadados relevantes, por exemplo, o URL do recurso que falhou ao baixar. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Código</b></th> 
   <th colname="2" class="entry"><b>Nome</b></th> 
   <th colname="3" class="entry"><b>InnerNotification&gt;/b&gt;</th> 
   <th colname="4" class="entry"><b>Chaves de metadados</b></th> 
   <th colname="5" class="entry"><b>Comentários</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Resolução de anúncios</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET, INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao tentar carregar um anúncio criativo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_ RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR, AD_ID,DESCRIÇÃO</span> </td> 
   <td colname="5"> <p>Falha na resolução do anúncio devido a um URL VAST inválido ou porque nenhum anúncio foi retornado do invólucro VAST. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifestações em segundo plano</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> ANTECEDENTE_MANIFEST_AVISO</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_ERROR</span> BACKGROUND_MANIFEST_ WARNING_NAME <span class="codeph"></span> <span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> <p> Erro no download do manifesto em segundo plano. Qualquer problema ao atualizar o manifesto em segundo plano é despachado como um aviso TVSDK e não faz com que a reprodução pare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_WARNING</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> <p></p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>TimeRangeCollection</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210000 </span> </td> 
   <td colname="2"><span class="codeph"> UNDEFINED_ TIME_RANGES </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> O modo de sinalização de anúncio é definido como intervalos personalizados, mas não há intervalos definidos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_TIME_ RANGES </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> <p> Um ou mais intervalos de tempo são inválidos e serão ignorados ou modificados. </p> <p> DESCRIÇÃO é uma string que contém a descrição dos intervalos inválidos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Específico do iOS</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>O AD não foi inserido no fluxo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_AUDIOONLY_MISSING </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>O anúncio não contém fluxo somente de áudio </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_MATCHING_BITRATE_MISSING </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>Nenhum fluxo de anúncio correspondente encontrado para a taxa de bits atual do conteúdo. </p> <p>  </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270005 </span> </td> 
   <td colname="2"><span class="codeph"> AVASSET_FAILED_TO_CREATE </span> </td> 
   <td colname="3"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>Erro ao criar o AVAsset. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270006 </span> </td> 
   <td colname="2"><span class="codeph"> SITECATALYST_AVISO </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> <p>Aviso: Consulte a descrição do aviso do SiteCatalyst. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270007 </span> </td> 
   <td colname="2"><span class="codeph"> NETWORK_ERROR </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> <p>Erro ao obter dados da rede. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID e fonte (URL) podem ser recuperados pelo PTAdAsset nos metadados de notificação com a `AD_ASSET` chave.
>
>O [] atributo especifica uma chave opcional para notificação.
