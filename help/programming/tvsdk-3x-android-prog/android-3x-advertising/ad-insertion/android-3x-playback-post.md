---
description: O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço ou retrocesso e publicidade.
title: Comportamento de reprodução padrão e personalizado com anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Comportamento de reprodução padrão e personalizado com anúncios {#default-and-customized-playback-behavior-with-ads}

O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço ou retrocesso e publicidade.

Para substituir o comportamento padrão, use `AdBreakPolicySelector` .

>[!IMPORTANT]
>
>O TVSDK não fornece uma maneira de desativar a busca durante os anúncios. O Adobe recomenda que você configure seu aplicativo para desativar a busca durante os anúncios.

Este é o comportamento de reprodução do conteúdo ao vivo/linear:

* Retomar a reprodução após uma pausa resulta na reprodução do conteúdo que foi armazenado em buffer no momento da pausa.

   Se a posição de retomada ainda estiver no intervalo de reprodução, a reprodução deverá ser contínua. Caso contrário, o TVSDK vai para o novo ponto ativo. Também é possível executar uma operação de busca e selecionar um ponto de reprodução diferente.
* O TVSDK resolve os anúncios entre as dicas após a posição em que o aplicativo entra na reprodução em tempo real.

   A reprodução começa depois que a primeira dica é resolvida. O valor padrão para inserir a reprodução em tempo real é o ponto ativo do cliente, mas você pode escolher uma posição diferente. Todas as dicas antes da posição inicial são resolvidas depois que o aplicativo realiza uma busca na janela DVR.

A tabela a seguir descreve como o TVSDK lida com anúncios e quebras de anúncios durante a reprodução:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Atividade de vídeo</b> </th> 
   <th colname="col2" class="entry"> <b>Política de comportamento padrão do TVSDK</b> </th> 
   <th colname="col3" class="entry"><b>Personalização disponível por meio de  <span class="codeph"> AdBreakPolicySelector</b></span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante a reprodução normal, um ad break é encontrado. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> Para linhas/ao vivo, reproduz o ad break, mesmo que o ad break já tenha sido assistido. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">Para VOD, reproduz o ad break e marca o ad break como observado. </li> 
    </ul> </td> 
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
   <td colname="col3">Selecione quais das quebras ignoradas serão reproduzidas usando <span class="codeph"> selectAdBreaksToPlay</span> e determine quais quebras já foram observadas usando <span class="codeph"> AdBreak.isWatched</span> . <p>Importante:  Por padrão, o TVSDK marca um ad break como observado imediatamente após inserir o primeiro anúncio no ad break. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo avança ou retroage em um ou mais ad breaks e cai em um ad break observado. </td> 
   <td colname="col2"> Ignora o ad break e busca a posição imediatamente após o ad break. </td> 
   <td colname="col3">Especifique uma política de publicidade diferente para o ad break (com o status observado definido como true) e para o anúncio específico em que a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo entra no modo de peça (DVR). A taxa de reprodução pode ser negativa (retrocesso) ou maior que 1 (avançar rapidamente). </td> 
   <td colname="col2"> Ignora todos os anúncios durante um avanço rápido ou retrocesso, reproduz o último intervalo ignorado após o término da reprodução de truques e ignora a posição da reprodução de truques selecionada pelo usuário quando essa quebra termina a reprodução. </td> 
   <td colname="col3">Selecione quais das quebras ignoradas serão reproduzidas depois que a reprodução de truque terminar usando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo avança com anúncios que foram inseridos usando marcadores de anúncio personalizados. </td> 
   <td colname="col2"> Ignora a posição de busca selecionada pelo usuário. </td> 
   <td colname="col3">Para obter mais informações, consulte <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Exibir uma barra de movimentação com a posição de reprodução atual</a>. </td> 
  </tr> 
 </tbody> 
</table>

