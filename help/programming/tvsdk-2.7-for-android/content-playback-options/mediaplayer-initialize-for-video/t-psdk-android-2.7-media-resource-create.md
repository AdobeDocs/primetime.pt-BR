---
description: A classe MediaResource representa o conteúdo a ser carregado pela instância MediaPlayer.
seo-description: A classe MediaResource representa o conteúdo a ser carregado pela instância MediaPlayer.
seo-title: Criar um recurso de mídia
title: Criar um recurso de mídia
uuid: f34a11a3-dac2-405e-8632-1d9617cc019d
translation-type: tm+mt
source-git-commit: 1b7ec3759561159c55018b4b81f896ecc99a25e8

---


# Criar um recurso de mídia {#create-a-media-resource}

Para cada novo conteúdo de vídeo, inicialize uma instância MediaResource com informações sobre o conteúdo de vídeo e carregue o recurso de mídia.

A classe MediaResource representa o conteúdo a ser carregado pela instância MediaPlayer.

1. Crie um `MediaResource` enviando informações sobre a mídia para o `MediaResource` construtor.

   O `MediaResource` construtor exige os seguintes parâmetros:

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
      <td colname="col2"> Um dos seguintes membros da enumeração <span class="codeph"> MediaResource.Type </span> , correspondente ao tipo de arquivo indicado:
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - formato de arquivo de mídia base ISO (MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH </span> - Descrição da apresentação da mídia MPEG-DASH (MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> metadados </span> </td>
      <td colname="col2"> Uma instância da classe <span class="codeph"> Metadata </span> (uma estrutura semelhante a um dicionário), que pode conter informações adicionais sobre o conteúdo que está prestes a ser carregado, como conteúdo alternativo ou anúncio para colocar dentro do conteúdo principal. Se estiver usando publicidade, configure <span class="codeph"> AuditudeSettings </span> antes de usar este construtor. </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >O TVSDK suporta reprodução somente para tipos específicos de conteúdo. Se você tentar carregar qualquer outro tipo de conteúdo, o TVSDK enviará um evento de erro.
   >
   >Para conteúdo de VOD (Video-on-demand) MP4, o TVSDK não oferece suporte para reprodução de truques, streaming de taxa de bits adaptável (ABR), inserção de anúncios, legendas fechadas ou DRM.

   O código a seguir cria uma `MediaResource` instância:

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   A qualquer momento após essa etapa, você pode usar `MediaResource` acessadores (getters) para examinar o tipo, URL e metadados do recurso.

1. Carregue o recurso de mídia usando uma das seguintes opções:

   * A instância MediaPlayer.
   * `MediaPlayerItemLoader` Para obter mais informações, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >Não carregue o recurso de mídia em um thread em segundo plano. A maioria das operações TVSDK precisam ser executadas no thread principal, e executá-las em um thread em segundo plano pode fazer com que a operação emita um erro e saia.
