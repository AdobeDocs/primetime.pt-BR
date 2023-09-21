---
description: O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço ou retrocesso e publicidade.
title: Comportamento de reprodução padrão e personalizado com anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Comportamento de reprodução padrão e personalizado com anúncios {#default-and-customized-playback-behavior-with-ads}

O comportamento da reprodução de mídia é afetado pela busca, pausa, avanço ou retrocesso e publicidade.

Para substituir o comportamento padrão, use `AdBreakPolicySelector` .

>[!IMPORTANT]
>
>O TVSDK não fornece uma maneira de desativar a busca durante os anúncios. A Adobe recomenda configurar seu aplicativo para desativar a busca durante os anúncios.

Este é o comportamento de reprodução para conteúdo dinâmico/linear:

* Retomar a reprodução após uma pausa resulta na reprodução do conteúdo que estava em buffer no momento da pausa.

  Se a posição de retomada ainda estiver no intervalo de reprodução, a reprodução deverá ser contínua. Caso contrário, o TVSDK saltará para o novo ponto ativo. Também é possível executar uma operação de busca e selecionar um ponto de reprodução diferente.
* O TVSDK resolve anúncios entre dicas após a posição em que o aplicativo entra na reprodução ao vivo.

  A reprodução começa após a primeira indicação ser resolvida. O valor padrão para inserir a reprodução ao vivo é o ponto ao vivo do cliente, mas você pode escolher uma posição diferente. Todas as dicas antes da posição inicial são resolvidas depois que o aplicativo executa uma busca na janela DVR.

A tabela a seguir descreve como o TVSDK lida com anúncios e ad breaks durante a reprodução:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Atividade de vídeo</b> </th> 
   <th colname="col2" class="entry"> <b>Política de comportamento padrão do TVSDK</b> </th> 
   <th colname="col3" class="entry"><b>Personalização disponível por meio de <span class="codeph"> AdBreakPolicySelector</b></span> </th> 
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
   <td colname="col3">Selecione quais das interrupções ignoradas devem ser reproduzidas usando <span class="codeph"> selectAdBreaksToPlay</span> e determinar quais interrupções já foram assistidas usando <span class="codeph"> AdBreak.isWatched</span> . <p>Importante: por padrão, o TVSDK marca um ad break como assistido imediatamente após inserir o primeiro anúncio no ad break. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo busca um ou mais ad breaks e cai em um ad break assistido. </td> 
   <td colname="col2"> Ignora o ad break e busca a posição imediatamente após o ad break. </td> 
   <td colname="col3">Especifique uma política de anúncio diferente para o ad break (com o status observado definido como verdadeiro) e para o anúncio específico em que a busca terminou usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo entra em trick-play (modo DVR). A taxa de reprodução pode ser negativa (retrocesso) ou maior que 1 (avanço rápido). </td> 
   <td colname="col2"> Ignora todos os anúncios durante o avanço ou retrocesso rápido, reproduz o último intervalo ignorado após o término do truque e salta para a posição de jogo do truque selecionada pelo usuário quando esse intervalo termina a reprodução. </td> 
   <td colname="col3">Selecione quais das pausas ignoradas devem ser reproduzidas depois que a reprodução terminar usando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seu aplicativo procura anúncios que foram inseridos usando marcadores de anúncios personalizados. </td> 
   <td colname="col2"> Salta para a posição de busca selecionada pelo usuário. </td> 
   <td colname="col3">Para obter mais informações, consulte <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Exibir uma barra de limpeza de busca com a posição de reprodução atual</a>. </td> 
  </tr> 
 </tbody> 
</table>
