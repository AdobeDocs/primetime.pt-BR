---
description: Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes combinações de metadados de anúncio e modo de sinalização de anúncios. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.
title: Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncio{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes combinações de metadados de anúncio e modo de sinalização de anúncios. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.

>[!NOTE]
>
>Quando há um conflito entre os intervalos de tempo e os modos de sinalização de anúncios, o TVSDK dá prioridade aos intervalos de tempo.

**Quadro 3: Modo de sinalização/Comportamentos de combinação de metadados**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> Modo de sinalização do anúncio </th> 
   <th class="entry"> Metadados de anúncio </th> 
   <th class="entry"> Resolvedores Criados </th> 
   <th class="entry"><span class="codeph"> </span> InserementInformation - Rastreado </th> 
   <th class="entry"> Comportamento resultante </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>Mapa do servidor</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> Excluir </td> 
   <td> Excluir </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos excluídos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Excluir, Auditude </td> 
   <td> Excluir, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervalos excluídos, Anúncios inseridos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Anúncios inseridos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Substituir, Auditude </td> 
   <td> Excluir, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos substituídos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, nenhum anúncio inserido </td> 
  </tr> 
  <tr> 
   <td> <b>Casos de manifesto</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> Anúncios inseridos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Excluir, Auditude </td> 
   <td> Excluir, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervalos excluídos, publicidades inseridas </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Mark, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, nenhum anúncio inserido </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Excluir </td> 
   <td> Excluir </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos excluídos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Substituir, Auditude </td> 
   <td> Excluir, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos substituídos </td> 
  </tr> 
  <tr> 
   <td> <b>Intervalo de tempo personalizado</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Excluir </td> 
   <td> Excluir </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos excluídos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Excluir, Auditude </td> 
   <td> Excluir, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos excluídos, nenhum anúncio inserido </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> Nenhum </td> 
   <td> Nenhuma publicidade inserida </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Substituir, Auditude </td> 
   <td> Excluir, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos substituídos por anúncios </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Anúncio personalizado, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, nenhum anúncio inserido </td> 
  </tr> 
  <tr> 
   <td> <b>Not set (padrão)</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Excluir </td> 
   <td> Excluir </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos excluídos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Excluir, Auditude </td> 
   <td> Excluir, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Intervalos excluídos, publicidades inseridas </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Anúncios inseridos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Substituir, Auditude </td> 
   <td> Excluir, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos substituídos por anúncios </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
 </tbody> 
</table>

