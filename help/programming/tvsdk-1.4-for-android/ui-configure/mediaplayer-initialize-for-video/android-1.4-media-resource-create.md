---
description: Para cada novo conteúdo de vídeo, inicialize uma instância de MediaResource com informações sobre o conteúdo do vídeo e carregue o recurso de mídia. A classe MediaResource representa o conteúdo a ser carregado pela ocorrência MediaPlayer.
title: Criar um recurso de mídia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Criar um recurso de mídia {#create-a-media-resource}

Para cada novo conteúdo de vídeo, inicialize uma instância de MediaResource com informações sobre o conteúdo do vídeo e carregue o recurso de mídia. A classe MediaResource representa o conteúdo a ser carregado pela ocorrência MediaPlayer.

1. Criar um `MediaResource` transmitindo informações sobre a mídia para o `MediaResource` construtor.

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
    <td colname="col2"> <p>Um dos seguintes membros da <span class="codeph"> MediaResource.Type </span> enumeração que corresponde ao tipo de arquivo indicado: 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadados </p> </td> 
    <td colname="col2"> <p>Uma instância do <span class="codeph"> Metadados </span> que pode conter informações personalizadas sobre o conteúdo a ser carregado. </p> <p>Exemplos de conteúdo são conteúdo alternativo ou conteúdo de anúncio a ser colocado dentro do conteúdo principal. Se estiver usando anúncios, configure <span class="codeph"> ConfiguraçõesAuditoria </span>. Para obter mais informações, consulte <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Metadados de Ad Insertion </a>. </p> </td> 
    </tr> 
    </tbody> 
    </table>

   >[!IMPORTANT]
   >
   >O TVSDK oferece suporte à reprodução somente para tipos específicos de conteúdo. Se você tentar carregar qualquer outro tipo de conteúdo, o TVSDK enviará um evento de erro.
   >
   >Para conteúdo de vídeo sob demanda (VOD) MP4, o TVSDK não é compatível com truques, transmissão de taxa de bits adaptável (ABR), inserção de anúncios, legendas ocultas ou DRM.

   O código a seguir cria um `MediaResource` instância:

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
   >Nesse ponto, é possível usar `MediaResource` acessadores (getters) para examinar o tipo, o URL e os metadados do recurso.

1. Carregue o recurso de mídia usando o seguinte:

   * Sua instância do MediaPlayer.

     Para obter mais informações, consulte [Carregar um recurso de mídia no MediaPlayer](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Para obter mais informações, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >Não carregue o recurso de mídia em uma thread em segundo plano. A maioria das operações TVSDK precisa ser executada no thread principal, e executá-las em um thread em segundo plano pode fazer com que a operação gere um erro e saia.
