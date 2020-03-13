---
seo-title: Detalhes da notificação NATIVE_ERROR
title: Detalhes da notificação NATIVE_ERROR
uuid: 18c4da57-59de-41a8-a2ea-fef800565207
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Detalhes da notificação NATIVE_ERROR {#details-for-the-native-error-notification}

Quando o TVSDK lida com um erro nativo, ele define alguns ou todos os valores de chave de metadados a seguir.

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Nome da chave de metadados </th> 
   <th colname="col2" class="entry"> Valor dos metadados </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="col2"> 
    <ph>
      Código de erro nativo do AVE. 
    </ph> Esses códigos representam os seguintes: 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">Erros de DRM (códigos 3300 a 3367). São os mesmos códigos de erro equivalentes do Flash Player. </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">Erros de reprodução de vídeo (-1 a 89). </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">Erros de criptografia (300 a 307). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_NAME </span> </td> 
   <td colname="col2"> Uma string que contém o nome do erro; por exemplo, <span class="codeph"> AXS_InvalidVoucher </span> ou <span class="codeph"> DECODER_FAILED </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_SUBERROR_CODE </span> </td> 
   <td colname="col2"> Para erros de DRM, os códigos de suberro também são retornados. Esses códigos correspondem ao código de suberro <span class="codeph"> DRMErrorEvents </span> retornado pelo Flash Player. Ao relatar erros à Adobe, inclua este valor numérico para obter assistência para solução de problemas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING </span> </td> 
   <td colname="col2"> Para o DRM, esta é a sequência de erro personalizada da implantação do servidor DRM, se você tiver definido alguma. Também inclua isso ao relatar erros à Adobe. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DESCRIÇÃO </span> </td> 
   <td colname="col2"> Descrição da string do erro. Normalmente, o URL da mídia. </td> 
  </tr> 
 </tbody> 
</table>

O TVSDK recebe esses códigos de erro e strings do mecanismo de vídeo.

>[!IMPORTANT]
>
>Para obter uma lista completa dos códigos de erro do cliente DRM do Adobe Primetime, consulte Referência [de mensagem de erro do cliente](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf)DRM.