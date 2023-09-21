---
description: Essas classes fornecem informações que ajudam a determinar o desempenho do reprodutor.
title: Classes de QoS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Classes de QoS{#qos-classes}

Essas classes fornecem informações que ajudam a determinar o desempenho do reprodutor.

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> PTDeviceInformation</a> </td> 
   <td colname="2">Fornece informações sobre a plataforma e o sistema operacional em que o TVSDK é executado: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Versão do SO da plataforma </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Número de versão da biblioteca TVSDK </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Nome do modelo do dispositivo </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Nome do fabricante do dispositivo </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">UUID do dispositivo </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Largura/altura da tela do dispositivo </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlaybackInformation</a> </td> 
   <td colname="2"> Fornece informações sobre o desempenho da reprodução. Isso inclui a taxa de quadros, a taxa de bits do perfil, o tempo total gasto no buffering, o número de tentativas de buffering, o tempo necessário para obter o primeiro byte do primeiro fragmento de vídeo, o tempo necessário para renderizar o primeiro quadro, o tamanho do buffer no momento e o tempo de buffer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> ProvedorPTQ</a> </td> 
   <td colname="2">
    <pre>
      Fornece métricas de QoS essenciais para a reprodução e para o dispositivo.
    </pre>
    <pre>
      Classe do provedor de informações de QOS.
    </pre> </td> 
  </tr> 
 </tbody> 
</table>
