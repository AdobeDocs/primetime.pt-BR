---
description: Esta tabela fornece informações detalhadas sobre o AVISO. notificações do tipo .
title: Códigos de notificação de AVISO
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---


# Códigos de notificação de AVISO{#warning-notification-codes}

Esta tabela fornece informações detalhadas sobre o AVISO. notificações do tipo .

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
   <td colname="1"><span class="codeph"> 200000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION _FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR  </span><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO  </span> </td> 
   <td colname="5"> <p>Uma operação relacionada à reprodução falhou, mas a reprodução pode continuar. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Resolução de anúncios  </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_ RESOLVE_FAIL  </span><span class="codeph"> RESOURCE_PLACEMENT_ FAILED  </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID  </span> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>O resolvedor de anúncios falhou ao resolver/inserir o conteúdo do anúncio. A reprodução pode continuar. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifestações em segundo plano</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000  </span> </td> 
   <td colname="2"><span class="codeph"> AVISO_MANIFEST_DE_FUNDO</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_</span> <span class="codeph"> ERRORBACKGROUND_MANIFEST_ WARNING_</span> <span class="codeph"> NAMEDESCRIPTION</span> </td> 
   <td colname="5"> <p> Erro no download do manifesto em segundo plano. Qualquer problema ao atualizar o manifesto em segundo plano é enviado como um aviso TVSDK e não faz com que a reprodução pare. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001  </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_WARNING</span> </td> 
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
   <td colname="1" morerows="1"><span class="codeph"> 209100  </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING  </span> </td> 
   <td colname="3" morerows="1"> <p>Nenhum </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> NATIVE_ERROR_NAME  </span><span class="codeph"> DESCRIÇÃO  </span> </p> </td> 
   <td colname="5"> <p>A biblioteca AVE de baixo nível emitiu um erro. </p> <p>Consulte <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Detalhes para as notificações NATIVE_ERROR</a> para obter informações detalhadas sobre os valores desses campos de metadados. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_</span> <span class="codeph"> CODEDRM_ERROR_STRING</span> </p> </td> 
   <td colname="5">Código de erro secundário de DRM e sequência de erro do servidor DRM. Consulte <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Detalhes para as notificações NATIVE_ERROR</a> para obter informações detalhadas sobre os valores desses campos de metadados.
   </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Genérico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 29999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_WARNING  </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>Marca um evento de aviso genérico. Na verdade, não foi emitido pelo TVSDK. É apenas um marcador para o final do intervalo de códigos numéricos correspondente a eventos de aviso. </p> </td> 
  </tr> 
 </tbody> 
</table>

