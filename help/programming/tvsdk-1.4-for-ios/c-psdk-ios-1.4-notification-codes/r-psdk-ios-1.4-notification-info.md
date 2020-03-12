---
description: Esta tabela fornece informações detalhadas sobre notificações de tipo INFO.
seo-description: Esta tabela fornece informações detalhadas sobre notificações de tipo INFO.
seo-title: Códigos de notificação INFO
title: Códigos de notificação INFO
uuid: 10145ce6-9eb0-4829-85dd-1acfe97b07e8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Códigos de notificação INFO{#info-notification-codes}

Esta tabela fornece informações detalhadas sobre notificações de tipo INFO.

A maioria das notificações informativas contém metadados relevantes, por exemplo, o URL do recurso que falhou ao baixar. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Código </th> 
   <th colname="2" class="entry"> Nome </th> 
   <th colname="3" class="entry"> Notificação interna </th> 
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
   <td colname="1"><span class="codeph"> 300000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_START </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> A reprodução foi iniciada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> A reprodução foi concluída. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <p> Nenhum </p> </td> 
   <td colname="5"> Uma operação de busca foi iniciada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> Uma operação de busca foi concluída. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> O estado do player mudou. Quando o estado for ERROR (ERRO), a notificação interna será o objeto de notificação de erro que disparou o switch para o estado ERROR (ERRO). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Taxas de bits adaptáveis (ABR)</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000 </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> BITRATO </span> </td> 
   <td colname="5"> A taxa de bits do vídeo mudou. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Áudio de ligação tardia (LBA)</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>A faixa de áudio foi alterada. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Legendas</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 307000 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>O rastreamento de legendas mudou. </p> </td> 
  </tr> 
 </tbody> 
</table>

