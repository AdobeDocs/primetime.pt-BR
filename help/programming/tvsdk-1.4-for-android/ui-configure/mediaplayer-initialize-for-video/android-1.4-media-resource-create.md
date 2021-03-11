---
description: Para cada novo conteúdo de vídeo, inicialize uma instância MediaResource com informações sobre o conteúdo do vídeo e carregue o recurso de mídia. A classe MediaResource representa o conteúdo a ser carregado pela instância MediaPlayer.
title: Criar um recurso de mídia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Criar um recurso de mídia {#create-a-media-resource}

Para cada novo conteúdo de vídeo, inicialize uma instância MediaResource com informações sobre o conteúdo do vídeo e carregue o recurso de mídia. A classe MediaResource representa o conteúdo a ser carregado pela instância MediaPlayer.

1. Crie um `MediaResource` transmitindo informações sobre a mídia ao construtor `MediaResource`.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> Parâmetro do construtor </th> 
    <th colname="col2" class="entry"> Descrição </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>Uma string que representa o URL do manifesto/lista de reprodução da mídia. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>Um dos seguintes membros da enumeração <span class="codeph"> MediaResource.Type </span> que corresponde ao tipo de arquivo indicado: 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS  </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadados </p> </td> 
    <td colname="col2"> <p>Uma instância da classe <span class="codeph"> Metadados </span>, que pode conter informações personalizadas sobre o conteúdo a ser carregado. </p> <p>Exemplos de conteúdo são conteúdo alternativo ou de anúncio para colocar dentro do conteúdo principal. Se estiver usando publicidade, configure <span class="codeph"> AuditudeSettings </span>. Para obter mais informações, consulte <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Metadados de Ad Insertion </a>. </p> </td> 
    </tr> 
    </tbody> 
    </table>

   >[!IMPORTANT]
   >
   >O TVSDK suporta reprodução somente para tipos específicos de conteúdo. Se você tentar carregar qualquer outro tipo de conteúdo, o TVSDK enviará um evento de erro.
   >
   >Para conteúdo MP4 de vídeo sob demanda (VOD), o TVSDK não é compatível com reprodução de truques, streaming de taxa de bits adaptável (ABR), inserção de anúncios, legendas ocultas ou DRM.

   O código a seguir cria uma instância `MediaResource`:

   ```java
   try { 
       // create a MediaResource instance pointing to some HLS content 
       Metadata metadata = //TODO: create metadata  
       MediaResource mediaResource = MediaResource.createFromUrl( 
         "https://www.example.com/video/some-video.m3u8",  
         MediaResource.Type.HLS,  
         metadata); 
   } catch(IllegalArgumentException ex) { 
       // this exception is thrown if the URL does not point  
       // to a valid url. 
   } 
   ```

   >[!TIP]
   >
   >Neste ponto, você pode usar `MediaResource` acessadores (getters) para examinar o tipo do recurso, o URL e os metadados.

1. Carregue o recurso de mídia usando o seguinte:

   * Sua instância do MediaPlayer.

      Para obter mais informações, consulte [Carregar um recurso de mídia no MediaPlayer](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Para obter mais informações, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >Não carregue o recurso de mídia em um thread em segundo plano. A maioria das operações TVSDK precisam ser executadas no thread principal, e executá-las em um thread em segundo plano pode fazer com que a operação emita um erro e saia.
