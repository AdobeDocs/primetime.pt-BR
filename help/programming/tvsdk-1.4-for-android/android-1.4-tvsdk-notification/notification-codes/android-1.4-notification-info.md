---
description: Esta tabela fornece informações detalhadas sobre INFO. tipo de notificação.
title: Códigos de notificação INFO
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 4%

---

# Códigos de notificação INFO{#info-notification-codes}

Esta tabela fornece informações detalhadas sobre INFO. tipo de notificação.

<!--<a id="section_ED4302E363AE48CBA2C3E0B71AE612D8"></a>-->

A maioria das notificações informativas contém metadados relevantes, por exemplo, o URL do recurso que falhou no download. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

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
   <td colname="5"> Reprodução iniciada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> Reprodução concluída. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> Uma operação de busca foi iniciada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> Uma operação de busca foi concluída. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_CHANGE </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <span class="codeph"> CONTENT_ID</span> <span class="codeph"> CURRENT_MEDIA_TIME</span> </td> 
   <td colname="5"> O tempo de reprodução atual ultrapassou a borda entre o conteúdo principal e alternativo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>Qualquer notificação de ERRO. </p> </td> 
   <td colname="4"><span class="codeph"> ESTADO </span> </td> 
   <td colname="5"> O estado do player foi alterado. Quando o estado é ERROR, a notificação interna é o objeto de notificação de erro que acionou a alternância para o estado ERROR. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300006 </span> </td> 
   <td colname="2"><span class="codeph"> MARCADOR_DE_CONTEÚDO </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> Marcador de conteúdo recebido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300100 </span> </td> 
   <td colname="2"><span class="codeph"> LOAD_INFO_AVAILABLE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <span class="codeph"> FRAGMENT_URL</span> <span class="codeph"> FRAGMENT_SIZE</span> <span class="codeph"> FRAGMENT_DOWNLOAD_DURATION</span> <span class="codeph"> ÍNDICE_DE_PERÍODO</span> </td> 
   <td colname="5"> Fornece informações relacionadas à forma como os segmentos de vídeo estão sendo baixados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300101 </span> </td> 
   <td colname="2"><span class="codeph"> VIDEO_SIZE_CHANGED </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <span class="codeph"> ALTURA</span> <p><span class="codeph"> LARGURA</span> </p> </td> 
   <td colname="5"> O tamanho da janela de reprodução de vídeo foi alterado. </td> 
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
   <td colname="4"><span class="codeph"> TAXA DE BITS </span><span class="codeph"> CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> A taxa de bits do vídeo mudou. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Processamento de anúncios</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303000 </span> </td> 
   <td colname="2"><span class="codeph"> TIMELINE_CHANGE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span><span class="codeph"> ÍNDICE_DE_PERÍODO </span> </td> 
   <td colname="5"> A linha do tempo foi alterada (por exemplo, conteúdo alternativo foi adicionado ou removido). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_ PLACEMENT_COMPLETE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <span class="codeph"> PROPOSED_AD_BREAK</span> <span class="codeph"> ACCEPTED_AD_BREAK</span> </td> 
   <td colname="5"> Um ad break proposto foi aceito por <code>primetime-sdk-name</code> e colocados (em sua totalidade ou apenas parcialmente) na linha do tempo de reprodução. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_START </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> A reprodução de um ad break específico foi iniciada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_COMPLETE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> A reprodução de um ad break específico foi concluída. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303004 </span> </td> 
   <td colname="2"><span class="codeph"> AD_START </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANÚNCIO</span> </p> </td> 
   <td colname="5"> A reprodução de um anúncio específico foi iniciada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_COMPLETE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANÚNCIO</span> </p> </td> 
   <td colname="5"> A reprodução de um anúncio específico foi concluída. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_PROGRESS </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANÚNCIO</span> </p> <span class="codeph"> PROGRESSO</span> </td> 
   <td colname="5"> A reprodução de um anúncio específico atingiu uma certa porcentagem desse anúncio específico. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303007 </span> </td> 
   <td colname="2"><span class="codeph"> TIMED_METADATA_ADD </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <span class="codeph"> TIPO</span> <p><span class="codeph"> ID</span> </p> <span class="codeph"> NOME</span> <p><span class="codeph"> HORA</span> </p> </td> 
   <td colname="5"> Um novo metadado cronometrado foi descoberto no manifesto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303008 </span> </td> 
   <td colname="2"><span class="codeph"> AD_CLICK </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANÚNCIO</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> Retorna informações sobre um anúncio em que o usuário clicou. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303009</span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_SKIPPED</span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> ANÚNCIO</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> Um ad break foi ignorado. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname=""><b>Áudio de ligação tardia (LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> TRACK_ID </span><span class="codeph"> CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> A faixa de áudio foi alterada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 305000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_METADATA_AVAILABLE </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> PREFETCH_TIMESTAMP </span> </td> 
   <td colname="5"> Novos dados de DRM estão disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Genérico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 399999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_INFO </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>Marca um evento de informações genérico. Não emitido pelo TVSDK. É apenas um marcador para o final da gama de códigos numéricos correspondentes aos eventos informativos do TVSDK. </p> </td> 
  </tr> 
 </tbody> 
</table>
