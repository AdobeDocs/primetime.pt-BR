---
description: A classe MediaResource representa o conteúdo a ser carregado pela ocorrência MediaPlayer.
title: Criar um recurso de mídia
exl-id: 20515e90-cbe4-4945-823a-fe882ed460db
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Criar um recurso de mídia {#create-a-media-resource}

Para cada novo conteúdo de vídeo, inicialize uma instância de MediaResource com informações sobre o conteúdo do vídeo e carregue o recurso de mídia.

A classe MediaResource representa o conteúdo a ser carregado pela ocorrência MediaPlayer.

1. Criar um `MediaResource` transmitindo informações sobre a mídia para o `MediaResource` construtor.

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
      <td colname="col2"> <p>Um dos seguintes valores de string que correspondem ao tipo de arquivo indicado: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - Formato ISO de arquivo de mídia de base (MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> metadados</span> </td> 
      <td colname="col2"> <p>Uma instância do <span class="codeph"> Metadados</span> que pode conter informações personalizadas sobre o conteúdo a ser carregado. </p> <p>Exemplos de conteúdo são conteúdo alternativo ou conteúdo de anúncio a ser colocado dentro do conteúdo principal. Se estiver usando anúncios, configure <span class="codeph"> ConfiguraçõesAuditoria</span> antes de usar esse construtor. Para obter mais informações, consulte <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Metadados de Ad Insertion</a>. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >O TVSDK oferece suporte à reprodução somente para tipos específicos de conteúdo. Se você tentar carregar qualquer outro tipo de conteúdo, o TVSDK enviará um evento de erro.
   >
   >Para conteúdo de vídeo sob demanda (VOD) MP4, o TVSDK não é compatível com truques, transmissão de taxa de bits adaptável (ABR), inserção de anúncios, legendas ocultas ou DRM.

   O código a seguir cria um `MediaResource` instância:

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >Nesse ponto, é possível usar `MediaResource` acessadores (getters) para examinar o tipo, o URL e os metadados do recurso.

1. Carregue o recurso de mídia usando um dos seguintes:

   * Sua instância do MediaPlayer.

      Para obter mais informações, consulte [Carregar um recurso de mídia no MediaPlayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Para obter mais informações, consulte [Carregar um recurso de mídia no MediaPlayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
