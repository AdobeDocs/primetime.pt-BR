---
description: O comportamento da reprodução de mídia é afetado pela busca, pausa e inclusão de anúncios.
title: Comportamento de reprodução padrão e personalizado com anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Comportamento de reprodução padrão e personalizado com anúncios {#default-and-customized-playback-behavior-with-ads}

O comportamento da reprodução de mídia é afetado pela busca, pausa e inclusão de anúncios.

Para substituir o comportamento padrão, use `PTAdPolicySelector`.

>[!IMPORTANT]
>
>Para VOD e streaming ao vivo/linear, os ajustes da linha do tempo não podem ser revisados. Isso significa que um anúncio não pode ser removido da linha do tempo depois de ser reproduzido. Se o usuário retornar, o mesmo anúncio será reproduzido novamente mesmo que a política normal tenha sido removê-lo.

>[!IMPORTANT]
>
>O TVSDK não fornece uma maneira de desativar a busca durante os anúncios. O Adobe recomenda que você configure seu aplicativo para desativar a busca durante os anúncios.

A tabela a seguir descreve como o TVSDK lida com anúncios e quebras de anúncios durante a reprodução:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Atividade de vídeo</b></th> 
   <th colname="col2" class="entry"><b>Política de comportamento padrão do TVSDK</b></th> 
   <th colname="col3" class="entry"><b>Personalização disponível por meio do PTAdPolicySeletor</b></th>
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante a reprodução normal, um ad break é encontrado. </td> 
   <td colname="col2"></td> 
   <td colname="col3">Especifique uma política diferente para o ad break usando <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca o(s) ad break(s) em conteúdo principal. </td> 
   <td colname="col2"> Reproduz a última quebra de anúncio não assistida que foi ignorada e retoma a reprodução na posição de busca desejada quando a reprodução da quebra é concluída. </td> 
   <td colname="col3">Selecione qual quebra foi ignorada para reproduzir usando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca o(s) ad break(s) para o conteúdo principal. </td> 
   <td colname="col2"> Ignora a posição de busca desejada sem reproduzir ad breaks. </td> 
   <td colname="col3">Selecione qual quebra foi ignorada para reproduzir usando <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca um ad break. </td> 
   <td colname="col2"> Reproduz a partir do início do anúncio no qual a busca terminou. </td> 
   <td colname="col3">Especifique uma política de publicidade diferente para o ad break e para o anúncio específico em que a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca um anúncio de volta. </td> 
   <td colname="col2"> Reproduz a partir do início do anúncio no qual a busca terminou. </td> 
   <td colname="col3">Especifique uma política de publicidade diferente para o ad break e para o anúncio específico no qual a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca para frente ou para trás em ad break(s) assistido(s) em conteúdo principal. </td> 
   <td colname="col2"> Se o último ad break ignorado já tiver sido observado, ignora a posição de busca selecionada pelo usuário. </td> 
   <td colname="col3">Selecione quais das quebras ignoradas serão reproduzidas usando <span class="codeph"> selectAdBreaksToPlay</span> e determine quais quebras já foram observadas usando <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Importante:  Por padrão, o TVSDK marca um ad break como observado imediatamente após inserir o primeiro anúncio no ad break. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo avança ou retroage em um ou mais ad breaks e cai em um ad break observado. </td> 
   <td colname="col2"> Ignora o ad break e busca a posição imediatamente após o ad break. </td> 
   <td colname="col3">Especifique uma política de publicidade diferente para o ad break (com o status observado definido como true) e para o anúncio específico em que a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo avança com anúncios que foram inseridos usando marcadores de anúncio personalizados. </td> 
   <td colname="col2"> Ignora a posição de busca selecionada pelo usuário. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>