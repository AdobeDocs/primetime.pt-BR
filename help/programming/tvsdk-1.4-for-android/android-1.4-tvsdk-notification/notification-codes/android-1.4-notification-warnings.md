---
description: Esta tabela comprova informações detalhadas sobre notificações do tipo AVISO.
title: Códigos de notificação de AVISO
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---

# Códigos de notificação de AVISO {#warning-notification-codes}

Esta tabela comprova informações detalhadas sobre notificações do tipo AVISO.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

A maioria dos avisos contém metadados relevantes, por exemplo, o URL do recurso que falhou no download. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Código </th> 
   <th colname="2" class="entry"> Nome </th> 
   <th colname="3" class="entry"> NotificaçãoInterna </th> 
   <th colname="4" class="entry"> Chaves de metadados </th> 
   <th colname="5" class="entry"> Comentários </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Reprodução</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 200000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION _FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> <p>Uma operação relacionada à reprodução falhou, mas a reprodução pode continuar. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Resolução de anúncios</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_ RESOLVE_FAIL </span><span class="codeph"> RESOURCE_PLACEMENT_ FAILED </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID </span> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>O resolvedor de anúncios não conseguiu resolver/inserir o conteúdo do anúncio. A reprodução pode continuar. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET, ERRO_INTERNO</span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao tentar carregar um criativo de anúncio. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_ RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR, AD_ID,DESCRIÇÃO</span> </td> 
   <td colname="5"> <p>Falha na resolução do anúncio devido a um URL VAST inválido ou porque nenhum anúncio foi retornado do invólucro VAST. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifestos em segundo plano</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_ERROR</span> <span class="codeph"> BACKGROUND_MANIFEST_ WARNING_NAME</span> <span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> <p> Erro no download do manifesto em segundo plano. Qualquer problema ao atualizar o manifesto em segundo plano é despachado como um aviso TVSDK e não faz com que a reprodução pare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> AVISO_DE_BUSCA_INVÁLIDA</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100 </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING </span> </td> 
   <td colname="3" morerows="1"> <p>Nenhum </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> NATIVE_ERROR_NAME </span><span class="codeph"> DESCRIÇÃO </span> </p> </td> 
   <td colname="5"> <p>A biblioteca AVE de baixo nível emitiu um erro. </p> <p>Consulte <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Detalhes das notificações NATIVE_ERROR</a> para obter informações detalhadas sobre os valores desses campos de metadados. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span> <span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5"> Código de erro secundário DRM e string de erro do servidor DRM. Consulte <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Detalhes das notificações NATIVE_ERROR</a> para obter informações detalhadas sobre os valores desses campos de metadados.</td> 
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
   <td colname="2"><span class="codeph"> INTERVALOS_DE_TEMPO_INDEFINIDOS </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> O modo de sinalização de anúncios é definido como intervalos personalizados, mas não há intervalos definidos. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_TIME_ RANGES </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> <p> Um ou mais intervalos de tempo são inválidos e serão ignorados ou modificados. </p> <p> DESCRIÇÃO é uma cadeia de caracteres que contém a descrição dos intervalos inválidos. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Modo de truques</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 280000 </span> </td> 
   <td colname="2"><span class="codeph"> TRICKPLAY_RATE_ CHANGE_FAIL</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> <p> Falha na alteração de taxa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Genérico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_WARNING </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>Marca um evento de aviso genérico. Não emitido pelo TVSDK. É apenas um marcador para o final da faixa de códigos numéricos correspondentes aos eventos de aviso. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[OBSERVAÇÃO!] O adID e a origem (URL) podem ser recuperados por meio do PTAdAsset nos metadados de notificação com o `AD_ASSET` chave.
