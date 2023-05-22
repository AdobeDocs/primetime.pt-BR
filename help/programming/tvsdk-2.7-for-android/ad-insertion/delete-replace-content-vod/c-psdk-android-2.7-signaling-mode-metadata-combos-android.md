---
description: Você pode marcar, excluir e substituir intervalos de tempo em fluxos de VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Diferentes combinações de modo de sinalização e metadados resultam em comportamentos diferentes.
title: Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncios
exl-id: 949ca84f-4aa9-4668-b91b-99fdf13f625c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncios {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Você pode marcar, excluir e substituir intervalos de tempo em fluxos de VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Diferentes combinações de modo de sinalização e metadados resultam em comportamentos diferentes.

>[!TIP]
>
>Quando há um conflito entre intervalos de tempo e modos de sinalização de anúncio, o TVSDK atribui prioridade aos intervalos de tempo.

A tabela a seguir fornece os detalhes sobre o modo de sinalização e os comportamentos de combinação de metadados:

<table id="table_6044AA1ACFA244FA814EA2D0766C6D12"> 
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
   <td colname="1"> <p><b>Mapa do servidor</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
    <ul id="ul_E0A2F885E93B4D23A486C37B305E17D8"> 
     <li id="li_D977B398D3904A44AFEC4B05AB0E3340"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), </span> </li> 
     <li id="li_439886CB38AA46239C2E40352443888A"><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
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
   <td colname="1"> <p><b>Indicações de manifesto</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
    <ul id="ul_2DD298538E9344B9BAB882485BB57747"> 
     <li id="li_F39A69EFA7ED45C18978A2C462AF7641"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li id="li_8CCDA3B1C63F4BC396F28F443D8C42F8"><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
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
   <td colname="1"> <p><b>Intervalo de tempo personalizado</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td colname="1"> <p><b>Não definido (padrão)</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
