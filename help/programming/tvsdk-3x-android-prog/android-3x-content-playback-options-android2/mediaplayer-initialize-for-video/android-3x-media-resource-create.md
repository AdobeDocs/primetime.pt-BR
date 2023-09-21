---
description: A classe MediaResource representa o conteúdo a ser carregado pela ocorrência MediaPlayer.
title: Criar um recurso de mídia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Criar um recurso de mídia {#create-a-media-resource}

Para cada novo conteúdo de vídeo, inicialize uma instância de MediaResource com informações sobre o conteúdo do vídeo e carregue o recurso de mídia.

A classe MediaResource representa o conteúdo a ser carregado pela ocorrência MediaPlayer.

1. Criar um `MediaResource` transmitindo informações sobre a mídia para o `MediaResource` construtor.

   A variável `MediaResource` construtor requer os seguintes parâmetros:

   <table id="table_22886D6770FB45E99D35D0B90E6CC302"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Parâmetro do construtor </th> 
      <th colname="col2" class="entry"> Descrição </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> <span class="codeph"> url </span> </td> 
      <td colname="col2"> Uma string que representa o URL do manifesto/lista de reprodução da mídia. </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> type </span> </td> 
      <td colname="col2"> Um dos seguintes membros da <span class="codeph"> MediaResource.Type </span> enum, correspondente ao tipo de arquivo indicado: 
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282"> 
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li> 
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - Formato ISO de arquivo de mídia de base (MP4) </li> 
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> TRAÇO </span> - Descrição de apresentação de mídia MPEG-DASH (MPD) </li> 
      </ul> </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> metadados </span> </td> 
      <td colname="col2"> Uma instância do <span class="codeph"> Metadados </span> classe (uma estrutura semelhante a um dicionário), que pode conter informações adicionais sobre o conteúdo que está prestes a ser carregado, como conteúdo alternativo ou de anúncio para colocar dentro do conteúdo principal. Se estiver usando anúncios, configure <span class="codeph"> ConfiguraçõesAuditoria </span> antes de usar este construtor <a href="/help/programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-insertion-metadata/android-3x-ad-insertion-metadata.md"> Adicionar metadados de inserção </a>. </td> 
   </tr> 
   </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >O TVSDK oferece suporte à reprodução somente para tipos específicos de conteúdo. Se você tentar carregar qualquer outro tipo de conteúdo, o TVSDK enviará um evento de erro.
   >
   >Para conteúdo de vídeo sob demanda (VOD) MP4, o TVSDK não é compatível com truques, transmissão de taxa de bits adaptável (ABR), inserção de anúncios, legendas ocultas ou DRM.

   O código a seguir cria um `MediaResource` instância: >

   ```java
   // To do: Create metadata here 
   MediaResource res = new MediaResource( 
     "https://www.example.com/video/some-video.m3u8",  
   MediaResource.Type.HLS, 
     metadata); 
   ```

   A qualquer momento após essa etapa, você pode usar `MediaResource` acessadores (getters) para examinar o tipo, o URL e os metadados do recurso.

1. Carregue o recurso de mídia usando uma das seguintes opções:

   * A ocorrência MediaPlayer.
   * `MediaPlayerItemLoader` Para obter mais informações, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >Não carregue o recurso de mídia em uma thread em segundo plano. A maioria das operações TVSDK precisa ser executada no thread principal, e executá-las em um thread em segundo plano pode fazer com que a operação gere um erro e saia.
