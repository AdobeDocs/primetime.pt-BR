---
description: Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.
seo-description: Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.
seo-title: Efeito na inserção e exclusão de anúncios no modo de sinalização de anúncios e combinações de metadados de anúncios
title: Efeito na inserção e exclusão de anúncios no modo de sinalização de anúncios e combinações de metadados de anúncios
uuid: c2ae8148-889d-46ae-848a-5f45d993a0e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Efeito na inserção e exclusão de anúncios no modo de sinalização de anúncios e combinações de metadados de anúncios{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.

>[!NOTE]
>
>Quando há um conflito entre os intervalos de tempo e os modos de sinalização de anúncios, o TVSDK dá prioridade aos intervalos de tempo.

**Quadro 3: Modo de sinalização/Comportamentos de combinação de metadados**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> Modo de sinalização de anúncios </th> 
   <th class="entry"> Metadados de anúncio </th> 
   <th class="entry"> Resolvedores criados </th> 
   <th class="entry"><span class="codeph"> InserçãoInformações</span> criadas </th> 
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
   <td> Intervalos excluídos, Anúncios inseridos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Publicidades inseridas </td> 
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
   <td> <b>Casos de Manifesto</b> </td> 
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
   <td> Publicidades inseridas </td> 
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
   <td> Intervalos excluídos, anúncios inseridos </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Publicidades inseridas </td> 
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

