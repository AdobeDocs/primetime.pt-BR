---
description: Esta tabela fornece informações detalhadas sobre notificações de tipo de ERRO.
seo-description: Esta tabela fornece informações detalhadas sobre notificações de tipo de ERRO.
seo-title: Códigos de notificação de ERRO
title: Códigos de notificação de ERRO
uuid: cea75277-7747-4f9b-ad59-98f9f1a5ac2f
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
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 100000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO DE MAJOR_DRM_CODE </span><span class="codeph"> MINOR_DRM_CODE </span><span class="codeph"></span> </td> 
   <td colname="5"></td> 
  </tr> 
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
   <td colname="3"></td> 
   <td colname="4"></td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101001 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_PLAYBACK_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span><span class="codeph"> INTERNAL_ERROR </span><span class="codeph"> URL </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO</span> </td> 
   <td colname="5"> <p>Ocorreu um erro ao executar uma operação de busca. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>Ocorreu um erro ao executar uma operação de pausa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101101 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> <p>  </p> <p>  </p>
    <!-- workaround for PDF having too much negative kerning in column 2 --> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Recurso inválido</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102000 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_MEDIA_PLAYER_ITEM </span> </td> 
   <td colname="3"> <p>Nenhum </p> </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Processamento de anúncios</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_INVALID </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED</span> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>Falha na resolução do anúncio devido ao formato inválido de metadados do anúncio. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>A fase de resolução do anúncio falhou. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE </span> </td> 
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
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>Ocorreu um erro de nível baixo no iOS. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Configuração</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>Ocorreu um erro ao tentar alterar a visibilidade das faixas de CC. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ ERROR </span> </td> 
   <td colname="3"> <span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="4"> <p>Nenhum </p> </td> 
   <td colname="5"> <p>Ocorreu um erro ao tentar alterar as opções de estilização das faixas CC. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>iOS exclusivo</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_VERSION_INCOMPATÍVEL </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>A versão HLS dos anúncios é superior à versão HLS do conteúdo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170001 </span> </td> 
   <td colname="2"><span class="codeph"> ARGUMENT_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> <p>Erro de argumento </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170002 </span> </td> 
   <td colname="2"><span class="codeph"> M3U8_PARSER_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> <p>Não foi possível analisar m3u8. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170003 </span> </td> 
   <td colname="2"><span class="codeph"> WEBVTT_PARSER_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> <p>Não foi possível analisar o Webvtt. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170004 </span> </td> 
   <td colname="2"><span class="codeph"> HLS_SEGMENT_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span><span class="codeph"> URL </span><span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>O segmento excede a largura de banda especificada para a variante. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170005 </span> </td> 
   <td colname="2"><span class="codeph"> MBR_MEDIASEQUENCE_OFFSYNC </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> <p>O número de sequência de mídia não está sincronizado em todos os fluxos HLS deste MBR. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170006 </span> </td> 
   <td colname="2"><span class="codeph"> MISSING_FILE_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span><span class="codeph"> URL </span><span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>Arquivo ausente ou não respondendo. </p> <p>HTTP 404: Arquivo não encontrado. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170007 </span> </td> 
   <td colname="2"><span class="codeph"> AD_EMPTY_RESPONSE </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> <p>Não foi possível recuperar anúncios. Resposta vazia. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170008 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TIMEOUT </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> <p>Não foi possível recuperar anúncios. Erro de tempo limite. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170009 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="4"> Nenhum </td> 
   <td colname="5"> <p>Erro ao alterar o rastreamento de legendas. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170010 </span> </td> 
   <td colname="2"><span class="codeph"> SITECATALYST_ERROR </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"><span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="5"> <p>Erro do Site Catalyst. Consulte a descrição. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170011 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TARGET_DURATION_INCOMPATIBLE </span> </td> 
   <td colname="3"> Nenhum </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>A DURAÇÃO DO TARGET do anúncio é superior à DURAÇÃO DO TARGET do conteúdo. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE] A adID e a fonte (URL) podem ser recuperadas por meio do `PTAdAsset` nos metadados de notificação com a `AD_ASSET` chave.
