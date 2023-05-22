---
description: Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma intermitência curta de vídeo. O TVSDK do navegador pode selecionar o nível de qualidade para cada intermitência com base na largura de banda disponível.
title: Taxas de bits adaptáveis (ABR) para qualidade de vídeo
exl-id: 2506a57b-d77d-4bd1-9e4c-5e00ef1bc8b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# Visão geral {#adaptive-bit-rates-abr-for-video-quality-overview}

Os fluxos HLS e DASH fornecem codificações (perfis) de taxa de bits diferentes para a mesma intermitência curta de vídeo. O TVSDK do navegador pode selecionar o nível de qualidade para cada intermitência com base na largura de banda disponível.

O TVSDK do navegador monitora constantemente a taxa de bits para garantir que o conteúdo seja reproduzido na taxa de bits ideal para a conexão de rede atual.

Você pode definir a política de switching ABR (taxa de bits adaptável) e as taxas de bits inicial, mínima e máxima para um fluxo MBR (taxa de vários bits). O TVSDK do navegador alterna automaticamente para a taxa de bits que fornece a melhor experiência de reprodução na configuração especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Taxa de bits inicial </td> 
   <td colname="col2">A taxa de bits de reprodução desejada (em bits por segundo) para o primeiro segmento. Quando a reprodução começa, o perfil mais próximo, que é igual ou maior que a taxa de bits inicial, é usado para o primeiro segmento. <p> Se uma taxa de bits mínima for definida e a taxa de bits inicial for menor que a taxa mínima, o TVSDK do navegador selecionará o perfil com a taxa de bits mais baixa acima da taxa de bits mínima. Se a taxa inicial estiver acima da taxa máxima, o TVSDK do navegador selecionará a taxa mais alta abaixo da taxa máxima. </p> <p>Se a taxa de bits inicial for zero ou indefinida, a taxa de bits inicial será determinada pela política ABR. </p> <p><span class="codeph"> taxaDeBitsInicial</span> retorna um valor inteiro que representa o perfil byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa de bits mínima </td> 
   <td colname="col2">A taxa de bits mais baixa permitida para a qual o ABR pode alternar. A switching ABR ignora perfis com uma taxa de bits inferior a essa taxa de bits. <p><span class="codeph"> minBitRate</span> retorna um valor inteiro que representa o perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Taxa de bits máxima </td> 
   <td colname="col2">A taxa de bits mais alta permitida para a qual o ABR pode alternar. A switching ABR ignora perfis com uma taxa de bits superior a essa taxa de bits. <p><span class="codeph"> maxBitRate</span> retorna um valor inteiro que representa o perfil de bits por segundo. </p> </td> 
  </tr> 
 </tbody> 
</table>

Lembre-se das seguintes informações:

* Quando a taxa de bits muda, o TVSDK do navegador é enviado `AdobePSDK.ProfileEvent` com o tipo como `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* Você pode alterar as configurações do ABR a qualquer momento e o reprodutor alterna para usar o perfil que melhor corresponde às configurações mais recentes.

Por exemplo, se um fluxo tiver os seguintes perfis:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Se você especificar um intervalo de 300000 a 2000000, o TVSDK do navegador considerará apenas os perfis 1, 2 e 3. Isso permite que os aplicativos se ajustem a várias condições de rede, como alternar de wi-fi para 3G ou para vários dispositivos, como um telefone, um tablet ou um desktop.

Para definir parâmetros de controle ABR:

* Defina os parâmetros no `ABRControlParameters` classe.
