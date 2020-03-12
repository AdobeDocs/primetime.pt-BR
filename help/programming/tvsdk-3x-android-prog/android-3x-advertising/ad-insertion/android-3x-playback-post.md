---
description: O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço rápido ou retrocesso e publicidade.
seo-description: O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço rápido ou retrocesso e publicidade.
seo-title: Comportamento de reprodução padrão e personalizado com anúncios
title: Comportamento de reprodução padrão e personalizado com anúncios
uuid: f008eea1-f30f-4a7a-ad8b-9cde4bac121e
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Comportamento de reprodução padrão e personalizado com anúncios {#default-and-customized-playback-behavior-with-ads}

O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço rápido ou retrocesso e publicidade.

Para substituir o comportamento padrão, use `AdBreakPolicySelector` .

>[!IMPORTANT]
>
>O TVSDK não fornece uma maneira de desativar a busca durante os anúncios. A Adobe recomenda que você configure seu aplicativo para desativar a busca durante os anúncios.

Este é o comportamento de reprodução para conteúdo ao vivo/linear:

* A retomada da reprodução após uma pausa resulta na reprodução do conteúdo que foi armazenado em buffer no momento da pausa.

   Se a posição de retomada ainda estiver no intervalo de reprodução, a reprodução deve ser contínua. Caso contrário, o TVSDK vai para o novo ponto ativo. Você também pode executar uma operação de busca e selecionar um ponto de reprodução diferente.
* O TVSDK resolve os anúncios entre as dicas após a posição na qual o aplicativo entra na reprodução ao vivo.

   A reprodução começa após a primeira dica ser resolvida. O valor padrão para inserir a reprodução ao vivo é o ponto ativo do cliente, mas você pode escolher uma posição diferente. Todas as dicas antes da posição inicial são resolvidas depois que o aplicativo realiza uma busca na janela do DVR.

A tabela a seguir descreve como o TVSDK lida com anúncios e quebras de anúncios durante a reprodução:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Atividade de vídeo</b> </th> 
   <th colname="col2" class="entry"> <b>Política de comportamento TVSDK padrão</b> </th> 
   <th colname="col3" class="entry"><b>Personalização disponível por meio de <span class="codeph"> AdBreakPolicySelector</b></span> </th> 
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
   <td colname="col3">Selecione qual quebra foi ignorada para reproduzir usando <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
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
   <td colname="col3">Selecione quais das quebras ignoradas serão reproduzidas usando <span class="codeph"> AdBreaksToPlay</span> e determine quais quebras já foram observadas usando <span class="codeph"> AdBreak.isWatched</span> . <p>Importante:  Por padrão, o TVSDK marca uma quebra de anúncio como observado imediatamente após a entrada do primeiro anúncio no intervalo do anúncio. </p> </td> 
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
   <td colname="col3">Para obter mais informações, consulte <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Exibir uma barra de depuração de busca com a posição</a>de reprodução atual. </td> 
  </tr> 
 </tbody> 
</table>

