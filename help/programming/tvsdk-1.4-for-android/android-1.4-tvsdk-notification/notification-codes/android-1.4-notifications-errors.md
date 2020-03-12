---
description: Esta tabela fornece informações detalhadas sobre notificações de tipo de ERRO.
seo-description: Esta tabela fornece informações detalhadas sobre notificações de tipo de ERRO.
seo-title: Códigos de notificação de ERRO
title: Códigos de notificação de ERRO
uuid: cc21473d-924e-475d-96ea-352233f664ef
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Códigos de notificação de ERRO{#error-notification-codes}

Esta tabela fornece informações detalhadas sobre notificações de tipo de ERRO.

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

A maioria dos erros contém metadados relevantes, por exemplo, o URL do recurso que falhou ao baixar. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Código </th> 
   <th colname="2" class="entry"> Nome </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
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
   <td colname="1"><span class="codeph"> 101000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> Ocorreu um erro ao baixar um fragmento ou segmento (vídeo e áudio). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> DESIRED_SEEK_POSITION </span><span class="codeph"> DESIRED_SEEK_PERIOD </span> </td> 
   <td colname="5"> Ocorreu um erro ao executar uma operação de busca. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> Ocorreu um erro ao executar uma operação de pausa. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102 </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> Ocorreu um erro ao recuperar informações sobre um período de conteúdo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103 </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> Ocorreu um erro ao tentar recuperar a posição de reprodução. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104 </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> Ocorreu um erro ao tentar recuperar as informações do QOS. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200 </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> Ocorreu um erro ao tentar baixar dados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Recurso inválido</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102100 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span><span class="codeph"> RECURSO </span> </td> 
   <td colname="5"> Ocorreu um erro ao carregar um item de recurso. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_ FAILED </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span> </td> 
   <td colname="5"> Ocorreu um erro ao colocar um recurso na linha do tempo de reprodução. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Processamento de anúncios</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA_INVALID </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE </span> </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> Nenhum </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_INVALID </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> Falha na resolução do anúncio devido ao formato inválido de metadados do anúncio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="5"> Falha do plug-in de anúncio ao resolver anúncios. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> PROPOSTA_AD_BREAK</span> </td> 
   <td colname="5"> A fase de resolução do anúncio falhou. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Nativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <span class="codeph"> NATIVE_ERROR_CODE </span> NATIVE_ERROR_NAME <span class="codeph"> DESCRIÇÃO </span><span class="codeph"> </span> <span class="codeph"> DESCRIÇÃO</span> <p><b>Detalhes do DRM:</b> </p> <span class="codeph"> DRM_ERROR_STRING</span> <span class="codeph"> _NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>A biblioteca AVE de baixo nível emitiu um erro. </p> <p>Consulte <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Detalhes das notificações</a> NATIVE_ERROR para obter informações sobre os valores dessas chaves de metadados. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> Ocorreu um erro ao instanciar a biblioteca de baixo nível AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> Ocorreu um erro ao liberar a biblioteca de baixo nível AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_ RELEASE_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> Ocorreu um erro ao liberar os recursos de GPU utilizados pela biblioteca AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> Ocorreu um erro ao redefinir a biblioteca AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> Ocorreu um erro ao anexar uma exibição à biblioteca AVE. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Configuração</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107000 </span> </td> 
   <td colname="2"><span class="codeph"> SET_VOLUME_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> VOLUME DE DESCRIÇÃO </span> </td> 
   <td colname="5"> Ocorreu um erro ao tentar definir o nível do volume. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107001 </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_TIME_ ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span><span class="codeph"> PLAY_BUFFER_TIME </span> </td> 
   <td colname="5"> Ocorreu um erro ao tentar alterar os parâmetros de buffer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> Ocorreu um erro ao tentar alterar a visibilidade das faixas de CC. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> Ocorreu um erro ao tentar alterar as opções de estilização das faixas CC. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107004 </span> </td> 
   <td colname="2"><span class="codeph"> SET_ABR_PARAMETERS_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> Ocorreu um erro ao tentar alterar os parâmetros de controle ABR. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107005 </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_PARAMETERS_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span><span class="codeph"> INITIAL_BUFFER_TIME </span><span class="codeph"> PLAY_BUFFER_TIME </span> </td> 
   <td colname="5"> Ocorreu um erro ao tentar alterar os parâmetros de controle de buffering. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Áudio alternativo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK_NAME </span><span class="codeph"> AUDIO_TRACK_LANGUAGE </span> </td> 
   <td colname="5"> Ocorreu um erro relacionado a uma faixa de áudio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Genérico</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 199999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR</span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> Marca um evento de erro genérico. Não emitido pela TVSDK. Este é apenas um marcador para o fim do intervalo de códigos numéricos correspondente aos eventos de erro TVSDK. </td> 
  </tr> 
 </tbody> 
</table>

