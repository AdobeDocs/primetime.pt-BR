---
description: Ao registrar ouvintes de eventos no TVSDK do navegador, você especifica um tipo de evento para acompanhar e o nome do seu retorno de chamada. Quando um evento ocorre, o TVSDK do navegador chama o retorno de chamada e transmite para ele um objeto de evento do tipo apropriado.
title: Tipos e classes de evento para retornos de chamada
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Tipos e classes de evento para retornos de chamada{#event-types-and-classes-for-callbacks}

Ao registrar ouvintes de eventos no TVSDK do navegador, você especifica um tipo de evento para acompanhar e o nome do seu retorno de chamada. Quando um evento ocorre, o TVSDK do navegador chama o retorno de chamada e transmite para ele um objeto de evento do tipo apropriado.

<table frame="all" colsep="1" rowsep="1" id="table_FE58AD65AF3B4483816C00D7EAD2FB4F"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Ao ouvir esse nome de evento (AdobePSDK.EventType) </th> 
   <th class="entry">frases/browser-tvsdk-name transmite um evento de retorno de chamada desse tipo de objeto (<span class="codeph"> AdobePSDK.Event</span>) </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_kj4_jc4_2y"> 
     <li id="li_C00AD7DE32C94431A4550E21CAC1DCA5"><span class="codeph"> AD_STARTED</span> </li> 
     <li id="li_1A3EA7527B3642E9ADF39F3CC3D87EDC"><span class="codeph"> AD_PROGRESS</span> </li> 
     <li id="li_9FB16D4B43EC4905909E881BC1C86E74"><span class="codeph"> AD_COMPLETED</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> AdPlaybackEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_jpq_pc4_2y"> 
     <li id="li_782365D715684DDC835E16D08CC0BBDB"><span class="codeph"> AD_BREAK_STARTED</span> </li> 
     <li id="li_78D7EAEE99D04A35AD7C6EC60DDDC1CC"><span class="codeph"> AD_BREAK_COMPLETED</span> </li> 
     <li id="li_6155ADAF5E964C458E92AFFB4F7D6347"><span class="codeph"> AD_BREAK_SKIPPED</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> AdBreakPlaybackEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> AD_CLICK</span> </td> 
   <td><span class="codeph"> AdClickEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_eny_tc4_2y"> 
     <li id="li_13F95E4BF905425CA5A95ECC138CC078"><span class="codeph"> BUFFERING_BEGIN</span> </li> 
     <li id="li_BA6F4E38E2F440FAAA4E70DF906A3350"><span class="codeph"> BUFFERING_END</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> BufferEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> DRM_METADATA_INFO_AVAILABLE</span> </td> 
   <td><span class="codeph"> DRMMetadataInfoAvailableEvent</span> </td> 
  </tr> 
  <tr> 
   <td colname="2"><span class="codeph"> LOAD_INFORMATION_AVAILABLE</span> </td> 
   <td><span class="codeph"> LoadInformationEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_kwy_cd4_2y"> 
     <li id="li_D5455D287EA5472D95A45AD1A8835D61"><span class="codeph"> AUDIO_UPDATED</span> </li> 
     <li id="li_AFF5B14338AB4AA8B4DF3963F2FDD4CF"><span class="codeph"> LEGENDAS_ATUALIZADAS</span> </li> 
     <li id="li_F7C9B933C6A44E80B57EB5274640A17B"><span class="codeph"> MASTER_UPDATED</span> </li> 
     <li id="li_C9FDF852BF4F4B638A8A1CAAFC27A23F"><span class="codeph"> ITEM_CREATED</span> </li> 
     <li id="li_85E13B35A6DB44A4BA0F93EA52B9D08A"><span class="codeph"> ITEM_UPDATED</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> MediaPlayerItemEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> STATUS_CHANGED</span> </td> 
   <td><span class="codeph"> EventoDeAlteraçãoDeStatus</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> OPERATION_FAILED</span> </td> 
   <td><span class="codeph"> NotificationEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> RESERVA_ALCANÇADA</span> </td> 
   <td><span class="codeph"> EventoReserva</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_jfl_224_2y"> 
     <li id="li_02B430978FA14A41A000DF8F9A345793"><span class="codeph"> RATE_SELETED</span> </li> 
     <li id="li_1EDC0664B59E49448040DF312C928FAA"><span class="codeph"> RATE_PLAYING</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> EventoTaxaReprodução</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> PERFIL_ALTERADO</span> </td> 
   <td><span class="codeph"> ProfileEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> PLAY_START</span> </td> 
   <td><span class="codeph"> PSDKEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_nwg_w24_2y"> 
     <li id="li_7CABB2AD7AB140E3BD4061460987BA40"><span class="codeph"> SEEK_POSITION_ADJUSTED</span> </li> 
     <li id="li_D44BEC28BDBB408280F5AA77E06107B3"><span class="codeph"> SEEK_BEGIN</span> </li> 
     <li id="li_EC000CF7E3DF4BC18443E368E347E7ED"><span class="codeph"> SEEK_END</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> SeekEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> TAMANHO_DISPONÍVEL</span> </td> 
   <td><span class="codeph"> SizeAvailableEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> TIME_CHANGED</span> </td> 
   <td><span class="codeph"> EventoDeAlteraçãoDeTempo</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> TIMED_METADATA_AVAILABLE</span> </td> 
   <td><span class="codeph"> TimedMetadataEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> LINHA DO TEMPO_ATUALIZADA</span> </td> 
   <td><span class="codeph"> EventoDeLinhaDoTempo</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> PLAYBACK_RANGE_UPDATED</span> </td> 
   <td></td> 
  </tr> 
 </tbody> 
</table>
