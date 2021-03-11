---
description: A classe MediaResource representa o conteúdo a ser carregado pela instância MediaPlayer.
title: Criar um recurso de mídia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Criar um recurso de mídia {#create-a-media-resource}

Para cada novo conteúdo de vídeo, inicialize uma instância MediaResource com informações sobre o conteúdo do vídeo e carregue o recurso de mídia.

A classe MediaResource representa o conteúdo a ser carregado pela instância MediaPlayer.

1. Crie um `MediaResource` transmitindo informações sobre a mídia ao construtor `MediaResource`.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Parâmetro do construtor </th> 
      <th colname="col2" class="entry"> Descrição </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>Uma string que representa o URL do manifesto/lista de reprodução da mídia. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>Um dos seguintes valores de string que corresponde ao tipo de arquivo indicado: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span>  - Formato de arquivo de mídia base ISO (MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span>  - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> metadados</span> </td> 
      <td colname="col2"> <p>Uma instância da classe <span class="codeph"> Metadados</span>, que pode conter informações personalizadas sobre o conteúdo a ser carregado. </p> <p>Exemplos de conteúdo são conteúdo alternativo ou de anúncio para colocar dentro do conteúdo principal. Se estiver usando publicidade, configure <span class="codeph"> AuditudeSettings</span> antes de usar este construtor. Para obter mais informações, consulte <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Metadados de Ad Insertion</a>. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >O TVSDK suporta reprodução somente para tipos específicos de conteúdo. Se você tentar carregar qualquer outro tipo de conteúdo, o TVSDK enviará um evento de erro.
   >
   >Para conteúdo MP4 de vídeo sob demanda (VOD), o TVSDK não é compatível com reprodução de truques, streaming de taxa de bits adaptável (ABR), inserção de anúncios, legendas ocultas ou DRM.

   O código a seguir cria uma instância `MediaResource`:

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >Neste ponto, você pode usar `MediaResource` acessadores (getters) para examinar o tipo do recurso, o URL e os metadados.

1. Carregue o recurso de mídia usando uma das seguintes opções:

   * Sua instância do MediaPlayer.

      Para obter mais informações, consulte [Carregar um recurso de mídia no Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * Um `MediaPlayerItemLoader` Para obter mais informações, consulte [Carregar um recurso de mídia no Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).

