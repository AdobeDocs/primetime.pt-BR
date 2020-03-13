---
description: O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço rápido ou retrocesso (modo de reprodução de truque) e pela inclusão de publicidade.
seo-description: O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço rápido ou retrocesso (modo de reprodução de truque) e pela inclusão de publicidade.
seo-title: Comportamento de reprodução padrão e personalizado com anúncios
title: Comportamento de reprodução padrão e personalizado com anúncios
uuid: 45e6b0cd-fb0b-4896-b53a-d3bd78a3c1f3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# Comportamento de reprodução padrão e personalizado com anúncios{#default-and-customized-playback-behavior-with-ads}

O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço rápido ou retrocesso (modo de reprodução de truque) e pela inclusão de publicidade.

Para substituir o comportamento padrão, use `AdPolicySelector`.

>[!IMPORTANT]
>
>O TVSDK não fornece uma maneira de desativar a busca durante os anúncios. A Adobe recomenda que você configure seu aplicativo para desativar a busca durante os anúncios.

A tabela a seguir descreve como o TVSDK lida com anúncios e quebras de anúncios durante a reprodução:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Atividade de vídeo </th> 
   <th colname="col2" class="entry"> Política de comportamento TVSDK padrão </th> 
   <th colname="col3" class="entry">Personalização disponível por meio do <span class="codeph"> AdPolicySelector</span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante a reprodução normal, uma pausa de anúncio é encontrada. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> Para live/linear, reproduz o intervalo do anúncio, mesmo se o intervalo do anúncio já tiver sido observado. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">Para VOD, reproduz o intervalo do anúncio e marca o intervalo do anúncio como observado. </li> 
    </ul> </td> 
   <td colname="col3">Especifique uma política diferente para o intervalo do anúncio usando <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca encaminhar o(s) intervalo(s) do anúncio para o conteúdo principal. </td> 
   <td colname="col2"> Reproduz a última pausa de anúncio não assistida que foi ignorada e reinicia a reprodução na posição de busca desejada quando a(s) pausa(s) é(são) concluída(s). </td> 
   <td colname="col3">Selecione qual quebra foi ignorada para reproduzir usando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca o conteúdo principal em vez de quebra(s) de anúncio. </td> 
   <td colname="col2"> Vai para a posição de busca desejada sem reproduzir pausas de anúncio. </td> 
   <td colname="col3">Selecione qual quebra foi ignorada para reproduzir usando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca uma pausa de anúncio. </td> 
   <td colname="col2"> Reproduz a partir do início do anúncio no qual a busca terminou. </td> 
   <td colname="col3">Especifique uma política de publicidade diferente para o intervalo de publicidade e para o anúncio específico no qual a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca retroceder em uma pausa de anúncio. </td> 
   <td colname="col2"> Reproduz a partir do início do anúncio no qual a busca terminou. </td> 
   <td colname="col3">Especifique uma política de publicidade diferente para o intervalo de publicidade e para o anúncio específico no qual a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca encaminhar ou retroceder sobre quebra(s) de anúncios observados para o conteúdo principal. </td> 
   <td colname="col2"> Se a última quebra de anúncio ignorada já tiver sido observada, ignora a posição de busca selecionada pelo usuário. </td> 
   <td colname="col3">Selecione quais das quebras ignoradas serão reproduzidas usando <span class="codeph"> selectAdBreaksToPlay</span> e determine quais quebras já foram observadas usando <span class="codeph"> TimeLineItem.watched</span> . <p>Importante:  Por padrão, o TVSDK marca uma quebra de anúncio como observado imediatamente após a entrada do primeiro anúncio no intervalo do anúncio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca avançar ou retroceder em um ou mais anúncios quebrados e cai em um intervalo de anúncios observado. </td> 
   <td colname="col2"> Ignora o intervalo do anúncio e busca a posição imediatamente após o intervalo do anúncio. </td> 
   <td colname="col3">Especifique uma política de publicidade diferente para o intervalo (com o status observado definido como true) e para o anúncio específico no qual a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo entra no modo de peça (DVR). A taxa de reprodução pode ser negativa (rebobinar) ou maior que 1 (avançar rapidamente). </td> 
   <td colname="col2"> Ignora todos os anúncios durante um avanço rápido ou retrocesso, reproduz o último intervalo ignorado após o término da reprodução de truques e ignora a posição de reprodução de truques selecionada pelo usuário quando esse intervalo termina a reprodução. </td> 
   <td colname="col3">Selecione quais das quebras ignoradas serão reproduzidas após o término da reprodução do truque usando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca anúncios que foram inseridos usando marcadores de anúncio personalizados. </td> 
   <td colname="col2"> Ignora a posição de busca selecionada pelo usuário. </td> 
   <td colname="col3">Para obter mais informações, consulte <a href="../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Exibir uma barra de depuração de busca com a posição de reprodução atual...</a> </td> 
  </tr> 
 </tbody> 
</table>

