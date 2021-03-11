---
description: A classe MediaResource representa o conteúdo a ser carregado pela instância MediaPlayer.
title: Criar um recurso de mídia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Criar um recurso de mídia {#create-a-media-resource}

Para cada novo conteúdo de vídeo, inicialize uma instância MediaResource com informações sobre o conteúdo do vídeo e carregue o recurso de mídia.

A classe MediaResource representa o conteúdo a ser carregado pela instância MediaPlayer.

1. Crie um `MediaResource` transmitindo informações sobre a mídia ao construtor `MediaResource`.

   O construtor `MediaResource` requer os seguintes parâmetros:

   <table id="table_22886D6770FB45E99D35D0B90E6CC302"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Parâmetro do construtor </th> 
      <th colname="col2" class="entry"> Descrição </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> <span class="codeph"> url  </span> </td> 
      <td colname="col2"> Uma string que representa o URL do manifesto/lista de reprodução da mídia. </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> type  </span> </td> 
      <td colname="col2"> Um dos seguintes membros do enum <span class="codeph"> MediaResource.Type </span>, correspondente ao tipo de arquivo indicado: 
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282"> 
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS  </span> - M3U8 </li> 
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF  </span> - Formato de arquivo de mídia base ISO (MP4) </li> 
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH  </span> - Descrição de apresentação de mídia MPEG-DASH (MPD) </li> 
      </ul> </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> metadados  </span> </td> 
      <td colname="col2"> Uma instância da classe <span class="codeph"> Metadados </span> (uma estrutura semelhante a um dicionário), que pode conter informações adicionais sobre o conteúdo que está prestes a ser carregado, como conteúdo alternativo ou de anúncio para colocar no conteúdo principal. Se estiver usando publicidade, configure <span class="codeph"> AuditudeSettings </span> antes de usar este construtor <a href="/help/programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-insertion-metadata/android-3x-ad-insertion-metadata.md"> Metadados de inserção de anúncio </a>. </td> 
   </tr> 
   </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >O TVSDK suporta reprodução somente para tipos específicos de conteúdo. Se você tentar carregar qualquer outro tipo de conteúdo, o TVSDK enviará um evento de erro.
   >
   >Para conteúdo MP4 de vídeo sob demanda (VOD), o TVSDK não é compatível com reprodução de truques, streaming de taxa de bits adaptável (ABR), inserção de anúncios, legendas ocultas ou DRM.

   O código a seguir cria uma instância `MediaResource`:        >

   ```java
   // To do: Create metadata here 
   MediaResource res = new MediaResource( 
     "https://www.example.com/video/some-video.m3u8",  
   MediaResource.Type.HLS, 
     metadata); 
   ```

   A qualquer momento após essa etapa, você pode usar acessadores `MediaResource` (getters) para examinar o tipo de recurso, o URL e os metadados.

1. Carregue o recurso de mídia usando uma das seguintes opções:

   * A instância MediaPlayer.
   * `MediaPlayerItemLoader` Para obter mais informações, consulte  [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >Não carregue o recurso de mídia em um thread em segundo plano. A maioria das operações TVSDK precisam ser executadas no thread principal, e executá-las em um thread em segundo plano pode fazer com que a operação emita um erro e saia.
