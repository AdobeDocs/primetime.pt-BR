---
title: Detalhes da notificação NATIVE_ERROR
description: Detalhes da notificação NATIVE_ERROR
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Detalhes da notificação NATIVE_ERROR {#details-for-the-native-error-notification}

Quando o TVSDK lida com um erro nativo, ele define alguns ou todos os valores de chave de metadados a seguir.

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Nome da chave de metadados </th> 
   <th colname="col2" class="entry"> Valor de metadados </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="col2"> 
    <pre>
      Código de erro nativo do AVE. 
    </pre> Esses códigos representam o seguinte: 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">Erros DRM (códigos 3300 a 3367). Esses são os mesmos que os códigos de erro equivalentes do Flash Player. </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">Erros de reprodução de vídeo (-1 a 89). </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">Erros de criptografia (300 a 307). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_NAME </span> </td> 
   <td colname="col2"> Uma string que contém o nome do erro; por exemplo, <span class="codeph"> AXS_VoucherInválido </span> ou <span class="codeph"> DECODIFICADOR_FALHA </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_SUBERROR_CODE </span> </td> 
   <td colname="col2"> Para erros de DRM, os códigos de suberro também são retornados. Esses códigos correspondem à <span class="codeph"> DRMErrorEvents </span> código de suberro retornado pelo Flash Player. Ao relatar erros no Adobe, inclua esse valor numérico para obter assistência na solução de problemas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING </span> </td> 
   <td colname="col2"> Para o DRM, essa é a sequência de erro personalizada na implantação do servidor DRM, se você tiver definido alguma. Inclua também ao relatar erros no Adobe. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="col2"> Descrição da cadeia de caracteres do erro. Normalmente, o URL da mídia. </td> 
  </tr> 
 </tbody> 
</table>

O TVSDK recebe esses códigos de erro e strings do mecanismo de vídeo.

>[!IMPORTANT]
>
>Para obter uma lista completa dos códigos de erro do cliente Adobe Primetime DRM, consulte [Referência de mensagem de erro de cliente DRM](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf).
