---
description: Você pode marcar, excluir e substituir intervalos de tempo em fluxos de VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Diferentes combinações de modo de sinalização e metadados resultam em comportamentos diferentes.
title: Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncios
exl-id: 0b265471-2d5c-432b-b1c9-c850ce99f2f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncios{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Você pode marcar, excluir e substituir intervalos de tempo em fluxos de VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Diferentes combinações de modo de sinalização e metadados resultam em comportamentos diferentes.

>[!NOTE]
>
>Quando há um conflito entre intervalos de tempo e modos de sinalização de anúncio, o TVSDK atribui prioridade aos intervalos de tempo.

**Tabela 3: Comportamentos de combinação de modo de sinalização/metadados**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> Modo de sinalização de anúncio </th> 
   <th class="entry"> Metadados de publicidade </th> 
   <th class="entry"> Resolvedores Criados </th> 
   <th class="entry"><span class="codeph"> PlacementInformations</span> criado </th> 
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
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), </span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervalos excluídos, anúncios inseridos </td> 
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
   <td> Marcar </td> 
   <td> Anúncio personalizado </td> 
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
   <td> <b>Indicações de manifesto</b> </td> 
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
   <td> Intervalos excluídos, anúncios inseridos </td> 
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
   <td> Marcar </td> 
   <td> Anúncio personalizado </td> 
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
   <td> Nenhum anúncio inserido </td> 
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
   <td> Marcar </td> 
   <td> Anúncio personalizado </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Anúncio Personalizado, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, nenhum anúncio inserido </td> 
  </tr> 
  <tr> 
   <td> <b>Não definido (padrão)</b> </td> 
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
   <td> Intervalos excluídos, anúncios inseridos </td> 
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
   <td> Marcar </td> 
   <td> Anúncio personalizado </td> 
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
