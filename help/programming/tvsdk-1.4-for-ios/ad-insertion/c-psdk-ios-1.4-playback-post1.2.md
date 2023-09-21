---
description: O comportamento da reprodução de mídia é afetado pela busca, pausa e inclusão de publicidade.
title: Comportamento de reprodução padrão e personalizado com anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Comportamento de reprodução padrão e personalizado com anúncios{#default-and-customized-playback-behavior-with-ads}

O comportamento da reprodução de mídia é afetado pela busca, pausa e inclusão de publicidade.

Para substituir o comportamento padrão, use `PTAdPolicySelector`.

>[!IMPORTANT]
>
>Para VOD e transmissão ao vivo/linear, os ajustes da linha do tempo não podem ser revisados. Isso significa que um anúncio não pode ser removido da linha do tempo depois de ser reproduzido. Se o usuário buscar de volta, o mesmo anúncio será reproduzido mesmo se a política normal tivesse sido removê-lo.

>[!IMPORTANT]
>
>O TVSDK não fornece uma maneira de desativar a busca durante os anúncios. A Adobe recomenda configurar seu aplicativo para desativar a busca durante os anúncios.

A tabela a seguir descreve como o TVSDK lida com anúncios e ad breaks durante a reprodução:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Atividade de vídeo </th> 
   <th colname="col2" class="entry"> Política de comportamento padrão do TVSDK </th> 
   <th colname="col3" class="entry">Personalização disponível por meio de <span class="codeph"> PTAdPolicySelector</span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante a reprodução normal, um ad break é encontrado. </td> 
   <td colname="col2"></td> 
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
   <td colname="col3">Selecione quais das interrupções ignoradas devem ser reproduzidas usando <span class="codeph"> selectAdBreaksToPlay</span> e determinar quais interrupções já foram assistidas usando <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Importante: por padrão, o TVSDK marca um ad break como assistido imediatamente após inserir o primeiro anúncio no ad break. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca um ou mais ad breaks e cai em um ad break assistido. </td> 
   <td colname="col2"> Ignora o ad break e busca a posição imediatamente após o ad break. </td> 
   <td colname="col3">Especifique uma política de anúncio diferente para o ad break (com o status observado definido como verdadeiro) e para o anúncio específico em que a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo procura anúncios que foram inseridos usando marcadores de anúncios personalizados. </td> 
   <td colname="col2"> Salta para a posição de busca selecionada pelo usuário. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>
