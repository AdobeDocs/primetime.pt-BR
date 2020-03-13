---
description: Essas classes fornecem informações que ajudam a determinar o desempenho do player.
seo-description: Essas classes fornecem informações que ajudam a determinar o desempenho do player.
seo-title: Classes de QoS
title: Classes de QoS
uuid: c1f0218d-4a79-4141-9a74-e70ac4f70aa5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Classes de QoS {#qos-classes}

Essas classes fornecem informações que ajudam a determinar o desempenho do player.

Pacote: Pacote [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/package-summary.html) : [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">métricas.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> BufferingMetrics</a></span></td> 
   <td colname="2"> Fornece informações sobre quanto tempo o player permaneceu durante o buffering e a frequência com que um evento de buffering ocorreu. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> DeviceInformation</a> </span></td> 
   <td colname="2">Fornece informações sobre a plataforma e o sistema operacional em que a Frase é executada: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Versão do SO da plataforma </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Número da versão da biblioteca de frases </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Nome do modelo do dispositivo </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Nome do fabricante do dispositivo </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">UUID do dispositivo </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Largura/altura do ecrã do dispositivo </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/LoadInfo.html" format="html" scope="external"> LoadInfo</a></span> </td> 
   <td colname="2"> Contém várias informações de QoS sobre o carregamento de vários recursos (arquivos, manifesto ou lista de reprodução, fragmentos/segmentos, trilhas e assim por diante). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> ReproduçãoInformações</a></span> </td> 
   <td colname="2"> Fornece informações sobre o desempenho da reprodução. Isso inclui a taxa de quadros, a taxa de bits do perfil, o tempo total gasto no buffering, o número de tentativas de buffering, o tempo necessário para obter o primeiro byte do primeiro fragmento de vídeo, o tempo necessário para renderizar o primeiro quadro, a duração do buffer atual e o tempo do buffer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">métricas.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> Fornece informações sobre quanto tempo a mídia demorou para ser carregada, quanto tempo o player levou para renderizar o primeiro quadro ou, no caso de um erro, para falhar. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">métricas.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackMetrics</a> </span></td> 
   <td colname="2"> Fornece informações sobre como a reprodução está se comportando. Isso inclui a taxa de quadros, a taxa de bits, a duração do buffer e assim por diante. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">métricas.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> Fornece informações sobre quantos segundos o player gastou durante a reprodução e quanto tempo o vídeo esteve realmente na tela. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span></td> 
   <td colname="2">Fornece métricas de QoS essenciais para a reprodução e o dispositivo. Classe do provedor de informações QOS.</td> 
  </tr> 
 </tbody> 
</table>
