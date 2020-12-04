---
description: Os fluxos HLS e DASH fornecem codificações de taxa de bits diferentes (perfis) para a mesma sequência curta de vídeo. O TVSDK do navegador pode selecionar o nível de qualidade para cada rajada com base na largura de banda disponível.
seo-description: Os fluxos HLS e DASH fornecem codificações de taxa de bits diferentes (perfis) para a mesma sequência curta de vídeo. O TVSDK do navegador pode selecionar o nível de qualidade para cada rajada com base na largura de banda disponível.
seo-title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
uuid: 4c34fb7b-1bbd-4fa9-8929-d50e85a17396
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---


# Visão geral {#adaptive-bit-rates-abr-for-video-quality-overview}

Os fluxos HLS e DASH fornecem codificações de taxa de bits diferentes (perfis) para a mesma sequência curta de vídeo. O TVSDK do navegador pode selecionar o nível de qualidade para cada rajada com base na largura de banda disponível.

O TVSDK do navegador monitora constantemente a taxa de bits para garantir que o conteúdo seja reproduzido na taxa de bits ideal para a conexão de rede atual.

Você pode definir a política de switching de taxa de bits adaptável (ABR) e as taxas de bits inicial, mínima e máxima para um fluxo de taxa de bits múltipla (MBR). O TVSDK do navegador muda automaticamente para a taxa de bits que fornece a melhor experiência de reprodução na configuração especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Taxa de bits inicial </td> 
   <td colname="col2">A taxa de bits de reprodução desejada (em bits por segundo) para o primeiro segmento. Quando os start de reprodução, o perfil mais próximo, igual ou superior à taxa de bits inicial, é usado para o primeiro segmento. <p> Se uma taxa de bits mínima for definida e a taxa de bits inicial for inferior à taxa mínima, o TVSDK do navegador selecionará o perfil com a taxa de bits mais baixa acima da taxa de bits mínima. Se a taxa inicial estiver acima da taxa máxima, o TVSDK do navegador selecionará a taxa mais alta abaixo da taxa máxima. </p> <p>Se a taxa de bits inicial for zero ou indefinida, a taxa de bits inicial será determinada pela política ABR. </p> <p><span class="codeph"> </span> initialBitRaterretorna um valor inteiro que representa o perfil byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa mínima de bits </td> 
   <td colname="col2">A menor taxa de bits permitida para a qual o ABR pode alternar. A alternância ABR ignora perfis com uma taxa de bits inferior a essa taxa de bits. <p><span class="codeph"> </span> minBitRaterretorna um valor inteiro que representa o perfil bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa máxima de bits </td> 
   <td colname="col2">A maior taxa de bits permitida para a qual o ABR pode alternar. A comutação ABR ignora perfis com uma taxa de bits superior a essa taxa de bits. <p><span class="codeph"> </span> maxBitRaterretorna um valor inteiro que representa o perfil bits por segundo. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se das seguintes informações:

* Quando a taxa de bits muda, o TVSDK do navegador despacha `AdobePSDK.ProfileEvent` com o tipo como `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* Você pode alterar as configurações de ABR a qualquer momento, e o player muda para usar o perfil que mais corresponde às configurações mais recentes.

Por exemplo, se um fluxo tiver os seguintes perfis:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se você especificar um intervalo de 300000 a 2000000, o TVSDK do navegador considerará somente os perfis 1, 2 e 3. Isso permite que os aplicativos se ajustem a várias condições de rede, como mudar de wi-fi para 3G ou para vários dispositivos, como telefone, tablet ou desktop.

Para definir parâmetros de controle ABR:

* Defina os parâmetros na classe `ABRControlParameters`.

