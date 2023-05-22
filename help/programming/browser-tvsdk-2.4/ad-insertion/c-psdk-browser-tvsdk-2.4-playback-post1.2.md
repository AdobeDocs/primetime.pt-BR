---
description: O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço rápido ou retrocesso (modo de reprodução de truque) e pela inclusão de publicidade.
title: Comportamento de reprodução padrão e personalizado com anúncios
exl-id: 56544683-28a3-4720-bfd8-946cb09880aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Comportamento de reprodução padrão e personalizado com anúncios{#default-and-customized-playback-behavior-with-ads}

O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço rápido ou retrocesso (modo de reprodução de truque) e pela inclusão de publicidade.

Para substituir o comportamento padrão, use `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>O TVSDK do navegador não fornece uma maneira de desativar a busca durante os anúncios. A Adobe recomenda configurar seu aplicativo para desativar a busca durante os anúncios.

A tabela a seguir descreve como o TVSDK do navegador lida com anúncios e ad breaks durante a reprodução:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Atividade de vídeo </th> 
   <th colname="col2" class="entry"> Política de comportamento do TVSDK para navegador padrão </th> 
   <th colname="col3" class="entry">Personalização disponível por meio de <span class="codeph"> AdBreakPolicySelector </span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante a reprodução normal, um ad break é encontrado. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> Para live/linear, o reproduz o ad break, mesmo que o ad break já tenha sido assistido. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">Para VOD, o reproduz o ad break e marca o ad break como assistido. </li> 
    </ul> </td> 
   <td colname="col3">Especifique uma política diferente para o ad break usando <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo procura por ad break(s) no conteúdo principal. </td> 
   <td colname="col2"> Reproduz o último ad break não assistido que foi ignorado e reinicia a reprodução na posição de busca desejada quando a reprodução do ad break(s) é concluída. </td> 
   <td colname="col3">Selecione qual interrupção ignorada deve ser reproduzida usando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca retroativamente por ad break(s) no conteúdo principal. </td> 
   <td colname="col2"> Salta para a posição de busca desejada sem reproduzir ad breaks. </td> 
   <td colname="col3">Selecione qual interrupção ignorada deve ser reproduzida usando <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo procura por um ad break. </td> 
   <td colname="col2"> Reproduz a partir do início do anúncio em que a busca terminou. </td> 
   <td colname="col3">Especifique uma política de anúncio diferente para o ad break e para o anúncio específico em que a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> O aplicativo busca de volta em um ad break. </td> 
   <td colname="col2"> Reproduz a partir do início do anúncio em que a busca terminou. </td> 
   <td colname="col3">Especifique uma política de anúncio diferente para o ad break e para o anúncio específico em que a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca avançar ou retroceder os ad break(s) assistidos no conteúdo principal. </td> 
   <td colname="col2"> Se o último ad break ignorado já tiver sido observado, o pulará para a posição de busca selecionada pelo usuário. </td> 
   <td colname="col3">Selecione quais das interrupções ignoradas devem ser reproduzidas usando <span class="codeph"> selectAdBreaksToPlay</span> e determinar quais interrupções já foram assistidas usando <span class="codeph"> isWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca um ou mais ad breaks e cai em um ad break assistido. </td> 
   <td colname="col2"> Ignora o ad break e busca a posição imediatamente após o ad break. </td> 
   <td colname="col3">Especifique uma política de anúncio diferente para o ad break (com o status observado definido como verdadeiro) e para o anúncio específico em que a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo procura anúncios que foram inseridos usando marcadores de anúncios personalizados. </td> 
   <td colname="col2"> Salta para a posição de busca selecionada pelo usuário. </td> 
   <td colname="col3">Para obter mais informações, consulte <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Manipular busca ao usar a barra de busca</a> </td> 
  </tr> 
 </tbody> 
</table>

## Configuração de comportamentos de anúncio personalizados {#section_custom_ad_behaviors}

Você pode definir seu comportamento preferido na fábrica de conteúdo de anúncios no `retrieveAdPolicySelectorCallbackFunc` método. Você pode usar o `selectPolicyForAdBreak`, `selectWatchedPolicyForAdBreak`, `selectPolicyForSeekIntoAd`, e `selectAdBreaksToPlay` métodos na fábrica de conteúdo para selecionar uma política.
