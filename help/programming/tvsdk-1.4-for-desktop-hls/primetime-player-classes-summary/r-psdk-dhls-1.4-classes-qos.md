---
description: Essas classes fornecem informações que ajudam a determinar o desempenho do reprodutor.
title: Classes de QoS
exl-id: 7d8b2bb2-491d-4c36-a6b3-8f91cf2304aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Classes de QoS {#qos-classes}

Essas classes fornecem informações que ajudam a determinar o desempenho do reprodutor.

Pacote: [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/package-detail.html)  Pacote: [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> MétricasDeBuffer</a></span> </td> 
   <td colname="2"> Fornece informações sobre quanto tempo o reprodutor gastou durante o buffering e com que frequência um evento de buffering ocorreu. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> DeviceInformation</a></span> </td> 
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
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformation.html" format="html" scope="external"> LoadInformation</a></span> </td> 
   <td colname="2"> Contém várias informações de QoS sobre o carregamento de vários recursos (arquivos, manifesto ou lista de reprodução, fragmentos/segmentos, trilhas e assim por diante). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformationType.html" format="html" scope="external"> LoadInformationType</a></span> </td> 
   <td colname="2"> Classe de enumeração que lista valores possíveis para a propriedade type dos objetos LoadInformation. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> InformaçõesDeReprodução</a></span> </td> 
   <td colname="2"> Fornece informações sobre o desempenho da reprodução. Isso inclui a taxa de quadros, a taxa de bits do perfil, o tempo total gasto no buffering, o número de tentativas de buffering, o tempo necessário para obter o primeiro byte do primeiro fragmento de vídeo, o tempo necessário para renderizar o primeiro quadro, o tamanho do buffer no momento e o tempo de buffer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> Fornece informações sobre quanto tempo a mídia levou para carregar, quanto tempo o reprodutor levou para renderizar o primeiro quadro ou, em caso de erro, para falhar. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackMetrics.html" format="html" scope="external"> Métricas de reprodução</a></span> </td> 
   <td colname="2"> Fornece informações sobre o comportamento da reprodução. Isso inclui a taxa de quadros, a taxa de bits, o comprimento do buffer, etc. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> Fornece informações sobre quantos segundos o reprodutor gastou durante a reprodução e quanto tempo o vídeo esteve realmente na tela. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span> </td> 
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
