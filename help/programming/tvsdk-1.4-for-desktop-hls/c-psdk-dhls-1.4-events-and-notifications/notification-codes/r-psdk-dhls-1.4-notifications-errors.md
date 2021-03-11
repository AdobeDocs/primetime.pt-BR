---
description: Esta tabela fornece informações detalhadas sobre notificações do tipo ERROR.
title: Códigos de notificação de ERRO
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 4%

---


# Códigos de notificação de ERRO{#error-notification-codes}

Esta tabela fornece informações detalhadas sobre notificações do tipo ERROR.

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

A maioria dos erros contém metadados relevantes, por exemplo, o URL do recurso que falhou ao baixar. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
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
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 100000  </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR  </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE  </span><span class="codeph"> MINOR_DRM_CODE  </span><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5">Consulte também 106000 (
     <span class="codeph"> NATIVE_ERROR</span>).
   </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Reprodução</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR  </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR  </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>Ocorreu um erro ao baixar um fragmento ou segmento (vídeo e áudio). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101006  </span> </td> 
   <td colname="2"><span class="codeph"> SECURITY_ERROR  </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> URL  </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008</span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao executar uma operação de pausa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> DESIRED_SEEK_POSITION  </span><span class="codeph"> DESIRED_SEEK_PERIOD  </span> </td> 
   <td colname="5"> <p>Erro ao executar uma operação de busca. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102  </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Erro ao recuperar informações sobre um período de conteúdo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103  </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao tentar recuperar a posição da reprodução. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104  </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao tentar obter as informações do QOS. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200  </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> URL  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao tentar transferir dados. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Recurso inválido  </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102100  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span><span class="codeph"> DO RECURSO  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao carregar um item de recurso. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_FAILED  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao colocar um recurso na linha do tempo de reprodução. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Processamento de anúncios  </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA _INVALID  </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL  </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL  </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE  </span> </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> Nenhum </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_ INVALID  </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>Falha na resolução do anúncio devido ao formato de metadados de anúncio inválido. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_ FAIL  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span> </td> 
   <td colname="5"> <p>Falha do plug-in de anúncio ao resolver anúncios. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="3">Nenhum</td> 
   <td colname="4"><span class="codeph"> PROPOSTA_AD_BREAK</span> </td> 
   <td colname="5"> <p>Falha na fase de resolução do anúncio. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006  </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000  </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> RUNTIME_</span> <span class="codeph"> CODERUNTIME_CODE_</span> <span class="codeph"> MESSAGERESOURCE_</span> <span class="codeph"> URLRESOURCE_</span> <span class="codeph"> TYPERESOURCE_ID</span> <p><b>Detalhes do DRM:</b> </p> <span class="codeph"> DRM_ERROR_</span> <span class="codeph"> STRINGRUNTIME_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>A biblioteca AVE de baixo nível emitiu um erro. </p> <p>Consulte <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Detalhes para as notificações NATIVE_ERROR</a> para obter informações sobre os valores dessas chaves de metadados. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao instanciar a biblioteca de baixo nível AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao lançar a biblioteca de baixo nível AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_ RELEASE_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao lançar os recursos de GPU utilizados pela biblioteca AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao redefinir a biblioteca AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao anexar uma vista à biblioteca AVE. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Áudio alternativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR  </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK_NAME  </span><span class="codeph"> AUDIO_TRACK_LANGUAGE  </span> </td> 
   <td colname="5"> <p>Ocorreu um erro relacionado a uma faixa de áudio. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Genérico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 19999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR  </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> <p>Marca um evento de erro genérico. Na verdade, não foi emitido pelo TVSDK. É apenas um marcador para o final do intervalo de códigos numéricos correspondente a eventos de erro TVSDK. </p> </td> 
  </tr> 
 </tbody> 
</table>

