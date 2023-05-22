---
description: A classe MediaResource representa o conteúdo a ser carregado pela ocorrência MediaPlayer.
title: Criar um recurso de mídia
exl-id: ab66255d-7848-479a-a8cd-c6113cdd7749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Criar um recurso de mídia {#create-a-media-resource}

A classe MediaResource representa o conteúdo a ser carregado pela ocorrência MediaPlayer.

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
    <td colname="col2"> <p>Um dos seguintes membros da <span class="codeph"> MediaResource.Type </span> enumeração que corresponde ao tipo de arquivo indicado: </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - Formato ISO de arquivo de mídia de base (MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> TRAÇO </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadados </p> </td> 
    <td colname="col2"> <p>Uma instância do <span class="codeph"> Metadados </span> que pode conter informações personalizadas sobre o conteúdo a ser carregado. Exemplos de conteúdo são conteúdo alternativo ou conteúdo de anúncio a ser colocado dentro do conteúdo principal. Se estiver usando anúncios, configure <span class="codeph"> ConfiguraçõesAuditoria </span> antes de usar esse construtor. Para obter mais informações, consulte <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">Ad-insertion-metadata</a>. </p> <p>Dica: é possível forçar o fallback do Flash, se necessário, usando o <span class="codeph"> forceFlash </span> ao criar um recurso de mídia. Isso pode ser útil porque, atualmente, nem todos os recursos (como fluxos de trabalho de anúncio ao vivo) são compatíveis com o TVSDK do navegador. O fallback do Flash é usado para reproduzir conteúdo de vídeo. </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >O TVSDK do navegador é compatível com a reprodução somente para tipos específicos de conteúdo. Se você tentar carregar qualquer outro tipo de conteúdo, o TVSDK do navegador enviará um evento de erro.

   O código a seguir cria um `MediaResource` instância:

   ```js
   //create a MediaResource instance pointing to some HLS content 
   Metadata metadata = //TODO: create metadata here 
   mediaResource = new AdobePSDK.MediaResource ( 
         "https://www.example.com/video/some-video.m3u8", 
         AdobePSDK.MediaResourceType.HLS,  
         metadata);
   ```

   >[!TIP]
   >
   >A qualquer momento depois disso, você poderá usar `MediaResource` acessadores (getters) para examinar o tipo, o URL e os metadados do recurso.

1. Carregue sua instância do MediaPlayer. Para obter mais informações, consulte [Carregar um recurso de mídia no MediaPlayer](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
