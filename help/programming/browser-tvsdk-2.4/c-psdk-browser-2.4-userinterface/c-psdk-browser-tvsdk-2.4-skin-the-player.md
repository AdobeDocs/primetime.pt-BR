---
description: Você pode usar as informações a seguir para ajudá-lo a aplicar skin ao seu reprodutor. Para cada construção visual, os comportamentos correspondentes são mencionados no comportamento padrão.
title: Colocar a pele no reprodutor
exl-id: 4ad50f96-d174-401f-a731-21e5fbfdbe31
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# Colocar a pele no reprodutor {#skinning-the-player}

Você pode usar as informações a seguir para ajudá-lo a aplicar skin ao seu reprodutor. Para cada construção visual, os comportamentos correspondentes são mencionados no comportamento padrão.

>[!IMPORTANT]
>
>Os detalhes da atribuição de capa neste documento são para os elementos de interface padrão criados pela estrutura da interface do usuário. Se o player modificar esses elementos, os elementos de atribuição de capa também precisarão ser alterados.

## Divisores de contêiner {#section_99B0D598219D4150B57E97D5381B118F}

Estes são os estilos para os divs de contêiner:

>[!TIP]
>
>Essas unidades estão listadas no `common-styles.css` arquivo.

Estes são os estilos para a div principal:

<table id="table_AC5745DF725543ADBBCD68BA6130DF12"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><b>Div principal</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-main-video-div-style</span> </td> 
   <td colname="col2"> <p>O estilo da div principal na qual o vídeo é reproduzido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .pip-mode-ative</span> </td> 
   <td colname="col2"> <p>Usado quando o modo PIP está ativo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">O comportamento padrão é <span class="codeph"> videoBehavior</span>. </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>Picture in Picture (PIP)</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-pip-video-div</span> </td> 
   <td colname="col2"> <p>O estilo da div em que o vídeo PIP é reproduzido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .exibir como vídeo principal</span> </td> 
   <td colname="col2"> <p>Aplicado ao PIP inicial quando trocado e exibido como o vídeo principal. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><b>Visualização de vários vídeos</b> </p> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-multi-view-container</span> </td> 
   <td colname="col2"> <p>É usado na visualização de vários vídeos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-multi-view-view</span> </td> 
   <td colname="col2"> <p>Um estilo css comum que é colocado em cada vídeo na visualização múltipla. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .multiview</span> </td> 
   <td colname="col2"> <p>Quando o container que hospeda cada um dos vídeos em multiview está em multiview. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Vários controles {#section_E9E4A8E3AEBF4BDC89840B84B3B0E737}

Estes são os estilos para controles genéricos do player:

>[!TIP]
>
>Esses estilos estão listados na variável `default-controls.css` arquivo.

<table id="table_0ACB6BAB5DAD42DBBD18CA7C0385A261"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-control</span> </td> 
   <td colname="col2"> <p>Aplicável a todos os controles na barra de controle, exceto ao depurador e ao espaço </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-input-slider</span> </td> 
   <td colname="col2"> <p>Controles deslizantes de entrada </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-header</span> </td> 
   <td colname="col2"> <p>Cabeçalho dos painéis </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-vertical-list-menu-item</span> </td> 
   <td colname="col2"> <p>Lista de menus em estilo vertical </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-fill-spacer</span> </td> 
   <td colname="col2"> <p>Espaço na barra de controle </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> separador de ptp-hr</span> </td> 
   <td colname="col2"> <p>Separador de régua horizontal </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-title</span> </td> 
   <td colname="col2"> <p>Título dos painéis </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-panel-close-btn</span> </td> 
   <td colname="col2"> <p>Botão para fechar o painel </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-button-background</span> </td> 
   <td colname="col2"> <p>Plano de fundo de todos os botões </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-txt-control</span> </td> 
   <td colname="col2"> <p>Estilos padrão para controles de texto. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Barra de controle {#section_B683B51EC746484B9AA90CB481D637BD}

Estes são os estilos da barra de controle:

<table id="table_681E13F264674F849FAA2523EB65F094"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-control-bar</span> (comportamento padrão)</td>
   <td colname="col2"> <p>Aplicável à barra de controle </p> </td> 
  </tr> 
 </tbody> 
</table>

## Botões de recursos {#section_57FFD242FF674EA2867BCF6CA7F6B855}

>[!NOTE]
>
>As letras nas tabelas a seguir correspondem às letras nesta ilustração.

Estes são os estilos da barra de depuração:

<table id="table_2207AD72E72A47FFA03AC748F06A54FD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo (A) </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar</span> </td> 
   <td colname="col2"> <p>Barra de depuração na barra de controle </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-buffer-progress-bar</span> </td> 
   <td colname="col2"> <p>Barra de progresso do buffer na barra de limpeza </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-seek-to-bar</span> </td> 
   <td colname="col2"> <p>Estado da barra de depuração quando o usuário procura nela </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-playback-progress-bar</span> </td> 
   <td colname="col2"> <p>Estado da barra de depuração na reprodução normal </p> </td> 
  </tr>
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-progress-bar-play-head</span> </td>
   <td colname="col2"> <p>Reproduzir a cabeça na barra de limpeza ao reproduzir </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-ad-marker-bar</span> </td>
   <td colname="col2"> <p>Barra de marcadores de publicidade </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-scrub-bar .ptp-ad-marker</span> </td>
   <td colname="col2"> <p>Marcador de publicidade </p> </td>
  </tr>
 </tbody>
</table>

Os comportamentos padrão são:

* `scrubBarBehavior`
* `bufferProgressBarBehavior`
* `playHeadBehavior`
* `playProgressBarBehavior`
* `seekToBarBehavior`

## Botão Reproduzir/Pausar {#section_F1F40A948D0049C5A4D8EA5F2A475CAA}

Estes são os estilos do botão Reproduzir/pausar:

<table id="table_975C2293222A4782A8C75A6149C1AD27">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo B) </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause</span> </td>
   <td colname="col2"> <p>Botão Reproduzir pausa na barra de controle. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause-state</span> </td>
   <td colname="col2"> <p><span class="codeph"> ptp-btn-playpause</span> no estado pause </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-playpause.pause-state</span> </td> 
   <td colname="col2"> <p><span class="codeph"> ptp-btn-playpause</span> no estado reproduzir </p> </td>
  </tr>
 </tbody>
</table>

O comportamento padrão é `playPauseButtonBehavior`.

## Volume {#section_23E17BD2343948F8A2CEE1C8BEE2F874}

Estes são os estilos para configurar o botão de volume:

<table id="table_8F9831F36A4D427CA31C9FFA4173170D">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (C) </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><span class="codeph"> .ptp-volume-control</span>
     <ul id="ul_B12ADDFB83EA40FD8B4E92AF418AA4B4">
      <li id="li_7DA8143A69ED4E7D8A560B9FF75D6BA7"><span class="codeph"> .expandido</span> </li>
      <li id="li_D8CCAD45D81C4850B6903FE261833AE6"><span class="codeph"> .vertical</span> </li>
     </ul> </p> </td>
   <td colname="col2"> <p>Controle de volume na barra de controle
     <ul id="ul_2C60F018FDCB458885738AC378C02F61">
      <li id="li_6B19572B504A4BBF9C97DC29C0E92A1D">Quando o controle está em formato expandido </li>
      <li id="li_6489E422E1944D5194CBDFC8383D2F30">Quando o controle está na forma vertical </li>
     </ul> </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume</span> </td>
   <td colname="col2"> <p>Botão Volume na barra de controle </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.min-estado-volume</span> </td>
   <td colname="col2"> <p>Quando o volume estiver no estado mínimo </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> ptp-btn-volume.estado-mudo</span> </td>
   <td colname="col2"> <p>Quando o volume está no estado mudo </p> </td>
  </tr>
 </tbody>
</table>

Os comportamentos padrão são `volumeBehavior` e `muteButtonBehavior`.

Estes são os estilos do controle deslizante de volume:

<table id="table_E3DC93F8FC614C30AADAE259D18F10EF">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (D) </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-volume-controle deslizante</span> </td>
   <td colname="col2"> <p>O controle deslizante do volume. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-volume-hidden</span> </td>
   <td colname="col2"> <p>O controle deslizante do volume em um estado oculto. </p> </td>
  </tr>
 </tbody>
</table>

O comportamento padrão é `volumeSliderBehavior`.

## Retroceder {#section_06EE608FC54A4CF5B5DF9DC743CFC740}

Este é o estilo do botão de retrocesso:

<table id="table_0ACB116582D54B188E9F5B5C03D3A615">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (E) </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>O botão de retrocesso na barra de controle. </p> </td>
  </tr>
 </tbody>
</table>

O comportamento padrão é `rewindButtonBehavior`.

## Hora {#section_0E6549B3DF6D4C10947D445A5F8EEA7F}

Este é o estilo para exibir o tempo restante na barra de controle:

<table id="table_CEE62BFF5FB04FDCBBE1331E0D727EBA">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (F) </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-txt-display-time</span> </td>
   <td colname="col2"> <p>Exibe o tempo restante na barra de controle </p> </td>
  </tr>
</tbody>
</table>

O comportamento padrão é `timeRemainingBehavior`.

## Retrocesso rápido {#section_F6E6C65BD3BD493A89915DF9B92933BA}

Este é o estilo do botão de retrocesso rápido:

<table id="table_25BB4966B709402383AB6A6822FC1999">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (G) </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastrewind</span> </td>
   <td colname="col2"> <p>O botão de retrocesso rápido na barra de controle. </p> </td>
  </tr>
 </tbody>
</table>

O comportamento padrão é `fastRewindButtonBehavior`.

## Retrocesso lento {#section_38A22BB8681B430F8C6808C3BD21FB4E}

Este é o estilo do botão de retrocesso lento:

<table id="table_E623C374622A497C91E22333D77AF8F6">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (H) </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-lowrewind</span> </td>
   <td colname="col2"> <p>O botão de retrocesso lento na barra de controle. </p> </td>
  </tr>
 </tbody>
</table>

O comportamento padrão é `slowRewindButtonBehavior`.

## Avançar Lentamente {#section_92ACF092EECC4A5EAF6AA090C05E552E}

Este é o estilo do botão de avanço lento:

<table id="table_88C1CF5DB2D84EDBA01AC62B70509B08">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (I) </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-slow-forward</span> </td>
   <td colname="col2"> <p>O botão de avanço lento na barra de controle. </p> </td>
  </tr>
 </tbody>
</table>

O comportamento padrão é `slowForwardButtonBehavior`.

## Avançar {#section_F90ED8B3739B49ACAB1F12DF18F0E4D6}

Este é o estilo do botão de avanço rápido:

<table id="table_F166BD1E8B934B34AF3690BBBAD894B7">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo (J) </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-fastforward</span> </td>
   <td colname="col2"> <p>O botão de avanço rápido na barra de controle. </p> </td>
  </tr>
 </tbody>
</table>

O comportamento padrão é `fastForwardButtonBehavior`.

## Faixa de áudio {#section_1CDF4FA5A1C14DB6B9C96579FFA1057C}

Estes são os estilos para configurar a faixa de áudio:

<table id="table_22FC521D786B45EB84F230894FFECE79">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>Botão De Faixa De Áudio (K)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-audio-track</span> </td>
   <td colname="col2"> <p>O botão de faixa de áudio na barra de controle. </p> </td>
  </tr>
  <tr>
   <td colname="col1">O comportamento padrão é <span class="codeph"> audioTrackButtonBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>Painel de seleção de faixa de áudio (L)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-panel</span> </td> 
   <td colname="col2"> <p>O painel para selecionar a faixa de áudio. </p> </td>
  </tr>
  <tr>
   <td colname="col1">O comportamento padrão é <span class="codeph"> audioTrackSelectionPanelBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>Cabeçalho de seleção de faixa de áudio (M)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>O cabeçalho para o <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Menu De Seleção De Faixa De Áudio (N)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-menu</span> </td>
   <td colname="col2"> <p>Os itens de menu no <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
 </tbody>
</table>

## Compartilhamento {#section_B2ADC76E76304A68AD648A00A12B676E}

Estes são os estilos para configurar o compartilhamento:

<table id="table_3264C472809D462B8FC16680B96B1AC9">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>Botão Compartilhamento De Redes Sociais (O)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video</span> </td> 
   <td colname="col2"> <p>O botão de compartilhamento de redes sociais na barra de controle que será aberto <span class="codeph"> ptp-share-video-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1">O comportamento padrão é <span class="codeph"> shareVideoButtonBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Compartilhamento do painel de vídeo (P)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video-panel</span> </td>
   <td colname="col2"> <p>O painel que exibe as opções de compartilhamento em redes sociais. </p> </td>
  </tr>
  <tr>
   <td colname="col1">O comportamento padrão é <span class="codeph"> shareVideoPanelBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Menu de compartilhamento de vídeo (Q)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-audio-track-selection-header</span> </td>
   <td colname="col2"> <p>O cabeçalho para o <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .share-video-panel-menu</span> </td>
   <td colname="col2"> <p>O menu em <span class="codeph"> ptp-share-video-panel</span> que exibe todas as opções para compartilhar conteúdo nas redes sociais. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-share-video-panel-menu-item</span> </td>
   <td colname="col2"> <p>O item de menu no <span class="codeph"> share-video-panel-menu</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-facebook</span> </td>
   <td colname="col2"> <p>O item de menu que permite compartilhar conteúdo no Facebook. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-twitter</span> </td>
   <td colname="col2"> <p>O item de menu que permite compartilhar conteúdo no Twitter. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-google-plus</span> </td>
   <td colname="col2"> <p>O item de menu que permite compartilhar conteúdo no Google Plus. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-share-video-linkedin</span> </td>
   <td colname="col2"> <p>O item de menu que permite compartilhar conteúdo no LinkedIn. </p> </td>
  </tr>
 </tbody>
</table>

## Legendas codificadas {#section_A01BA68218564DA0B7D6BF51F045D7AB}

Estes são os estilos para configurar legendas ocultas:

<table id="table_777C7034C9424F8C841DABD480FFAC47">
 <thead>
  <tr>
   <th colname="col1" class="entry"> Estilo </th>
   <th colname="col2" class="entry"> Descrição </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td colname="col1"> <p><b>Botão Legendas ocultas (R)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-btn-closed-caption</span> </td>
   <td colname="col2"> <p>A variável <span class="uicontrol"> Legendas codificadas</span> na barra de controle. </p> </td>
  </tr>
  <tr>
   <td colname="col1">O comportamento padrão é <span class="codeph"> closedCaptionButtonBehavior</span>. </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .no-state</span> </td>
   <td colname="col2"> <p>As legendas foram habilitadas para um vídeo. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Painel Legendas Ocultas (S)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-panel</span> </td>
   <td colname="col2"> <p>O painel para legendas ocultas. </p> </td>
  </tr>
  <tr>
   <td colname="col1">O comportamento padrão é <span class="codeph"> closedCaptionLanguagePanelBehavior</span>. </td>
   <td colname="col2"> </td>
</tr>
  <tr>
   <td colname="col1"> <p><b>Idiomas Com Legendas Ocultas (T)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-language-panel:</span> </td>
   <td colname="col2"> <p>O cabeçalho para o <span class="codeph"> ptp-audio-track-selection-panel</span>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-language-menu: </span> </td>
   <td colname="col2"> <p>O menu no painel de legendas ocultas. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> <p><b>Opções de Legendas Codificadas (U)</b> </p> </td>
   <td colname="col2"> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-btn</span> </td>
   <td colname="col2"> <p>A variável <span class="uicontrol"> Opções</span> no painel opções de legendas ocultas. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-panel</span> </td>
   <td colname="col2"> <p>O painel Opções no painel de legendas ocultas. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-menu-item</span> </td>
   <td colname="col2"> <p>O item de menu no painel de legendas ocultas. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .selecionado</span> </td>
   <td colname="col2"> <p>No estado selecionado. </p> </td>
  </tr>
  <tr>
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-done-btn</span> </td> 
   <td colname="col2"> <p>A variável <span class="uicontrol"> Concluído</span> no cabeçalho do painel de opções de legendas ocultas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-closed-caption-options-menu</span> </td> 
   <td colname="col2"> <p>O menu Opções em legendas ocultas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-main-menu</span> </td> 
   <td colname="col2"> <p>O menu principal para as opções de legendas ocultas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-sub-menu</span> </td> 
   <td colname="col2"> <p>O submenu para as opções de legendas ocultas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-opacity-slider</span> </td> 
   <td colname="col2"> <p>O controle deslizante de opacidade para opções de legendas ocultas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-menu-separator</span> </td> 
   <td colname="col2"> <p>O separador de opções de legenda oculta. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-menu-item</span> </td> 
   <td colname="col2"> <p>A legenda oculta <span class="uicontrol"> Opções</span> item de menu. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-preview-panel</span> </td> 
   <td colname="col2"> <p>O painel de visualização de legendas ocultas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-footer</span> </td> 
   <td colname="col2"> <p>O rodapé de opções de legendas ocultas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-reset-button</span> </td> 
   <td colname="col2"> <p>A variável <span class="uicontrol"> Redefinir</span> no rodapé do painel de opções de legendas ocultas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ptp-closed-caption-options-apply-button</span> </td> 
   <td colname="col2"> <p>A variável <span class="uicontrol"> Aplicar</span> no rodapé do painel de opções de legendas ocultas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">O comportamento padrão é <span class="codeph"> closedCaptionOptionsPanelBehavior</span>. </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## Mais Opções (V) {#section_18E25CF8A8964FFD9026A8A833089CE3}

Estes são os estilos para configurar opções adicionais:
<table id="table_EC6EF88E2EDE4B8EBB1C14F87A6161FA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more-options</span> </td> 
   <td colname="col2"> <p>A variável <span class="uicontrol"> Mais opções</span> botão. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-more-options.ptp-control-bar-btn</span> </td> 
   <td colname="col2"> <p>A variável <span class="codeph"> ptp-btn-more-options</span> que são usados na barra de controle. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel</span> </td> 
   <td colname="col2"> <p>O painel de controle Mais opções. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu</span> </td> 
   <td colname="col2"> <p>O menu do painel de controle Mais opções. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-more-options-control-panel-menu-item</span> </td> 
   <td colname="col2"> <p>O item de menu do painel de controle Mais Opções. </p> </td> 
  </tr> 
 </tbody> 
</table>

O comportamento padrão é `moreOptionsButtonBehavior`.

## Botão PIP (W) {#section_1EE039DEA99541D391B30BD1DF72A83E}

Este é o estilo para a variável [!UICONTROL PIP<] botão:

<table id="table_EE2E882C87E24D39B8D5347686F29E55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-pip</span> </td> 
   <td colname="col2"> <p>O botão PIP na barra de controle. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">O comportamento padrão é <span class="codeph"> pipButtonBehavior</span>. </td> 
   <td colname="col2"> </td>
  </tr> 
 </tbody> 
</table>

## Tela cheia (X) {#section_158A19DFB30E4432A67E4A74A7CBA563}

Este é o estilo para configurar a tela cheia:

<table id="table_5941835F31AC4E9CBA9702AB8D813B8F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-fullscreen</span> </td> 
   <td colname="col2"> <p>A variável <span class="uicontrol"> Tela cheia</span> botão na barra de controle. </p> </td> 
  </tr> 
 </tbody> 
</table>

O comportamento padrão é `fullScreenButtonBehavior`.

## Truque (Y) {#section_AE6F83BB7EE2497FB13CD94A8316192D}

Este é o estilo para configurar o truque:

<table id="table_F1ADAC0A4B4E48669828690BDEB4BC09"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-control-bar-trick-play-rate</span> </td> 
   <td colname="col2"> <p>O componente de exibição da taxa de truques na barra de controle. </p> </td> 
  </tr> 
 </tbody> 
</table>

O comportamento padrão é `trickPlayRateDisplayBehavior`.

## Visualização múltipla (Z) {#section_58EFAE7263BA45D3A4E2AB7309A9CAA7}

Este é o estilo para configurar o multiview:

<table id="table_84B37D7410EE40DFA7A8BB8431C6DCF0"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-btn-multiview</span> </td> 
   <td colname="col2"> <p>A variável <span class="uicontrol"> MultiView</span> botão na barra de controle e o estado inicial de <span class="uicontrol"> Visualização múltipla</span> botão. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">O comportamento padrão é <span class="codeph"> multiViewButtonBehavior</span>. </td> 
   <td colname="col2"> </td> 
  </tr> 
 </tbody> 
</table>

## Miniatura {#section_0AFD932975634BB08387EEE7D3BFC438}

Este é o estilo para configurar miniaturas:

<table id="table_968136A8BBA042A7A8E79739B8F92F55"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-progress-bar-thumb-nail</span> </td> 
   <td colname="col2"> <p>A barra de progresso das miniaturas. </p> </td> 
  </tr> 
 </tbody> 
</table>

O comportamento padrão é `thumbnailPreviewBehavior`.

## Mensagens de erro {#section_AC9858EE1B5A4FF4947E383C663B6AB5}

Este é o estilo para configurar mensagens de erro:

<table id="table_7F4C156170DB4AFFA7DEE06F00449506"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel</span> </td> 
   <td colname="col2"> <p>O painel que exibe as mensagens de erro do player. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-icon</span> </td> 
   <td colname="col2"> <p>O ícone exibido no painel quando há uma mensagem de erro. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-error-message-panel-message</span> </td> 
   <td colname="col2"> <p>A mensagem de erro exibida. </p> </td> 
  </tr> 
 </tbody> 
</table>

O comportamento padrão é `errorMessagePanelBehavior`.

## Sobreposição de buffering {#section_2FE8FDE2599E42BAA7411D0D38FA0A88}

Este é o estilo para configurar miniaturas:

<table id="table_1FECE1DC29B8434B886751A29455F004"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ptp-buffering-overlay</span> </td> 
   <td colname="col2"> <p>O controle de sobreposição de buffering. </p> </td> 
  </tr> 
 </tbody> 
</table>

A sobreposição padrão é `bufferingOverlayBehavior`.

## Seletores específicos {#section_51F735AEF82E41E890FF59E031A0DB89}

Este é o estilo do botão de avanço rápido:

<table id="table_E77EDC7D227348E79C7E73FB5D46F992"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estilo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> .ad-break</span> </td> 
   <td colname="col2"> <p>O estado do painel de controle durante a reprodução do anúncio. </p> <p>Aplica-se ao seguinte: 
     <ul id="ul_D5076303DCD94D968682289823D1A9F2"> 
      <li id="li_4290C4B2D48546E3AD023BED6CAAE395"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_72A3D3E916E44A55BA170407EAB0527D"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_A0BAEBB0E01B402EB83E3CE9B92B15CC"><span class="codeph"> .ptp-btn-fastrewind</span> </li> 
      <li id="li_FDF2CEDB0A854098907FF9CBCF1A61C1"><span class="codeph"> .ptp-btn-slow-forward</span> </li> 
      <li id="li_CD2E14DB3DD64C10A253DA23FBE04A04"><span class="codeph"> .ptp-btn-slow-forward</span> </li> 
      <li id="li_A230359E8F7F4571A9EBFF0E4C2462D7"><span class="codeph"> .ptp-btn-lowrewind</span> </li> 
      <li id="li_5711A315872F4FA59FDDF0EF0AFD03C6"><span class="codeph"> .ptp-btn-more-options </span> </li> 
      <li id="li_71C8E76077A84ED590160AB5ABFCC0D7"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_4A3113C0360F4F708AAA96AB316FA057"><span class="codeph"> .ptp-btn-closed-caption </span> </li> 
      <li id="li_901A0186D65A48A1B774DC555CEC5367"><span class="codeph"> .ptp-btn-audio-track</span> </li> 
      <li id="li_2331583C01C2482B8EE72979FBF111DB"><span class="codeph"> .ptp-btn-pip </span> </li> 
      <li id="li_7BB39BDF5E294AEB8FA3DCD9F9A29468"><span class="codeph"> .ptp-btn-rewind</span> </li> 
      <li id="li_E4FEF5A7486A40F6A5FE1119BD63AFEF"><span class="codeph"> .ptp-scrub-bar</span> </li> 
      <li id="li_12153547558A4871842EE0416BCCA8B2"><span class="codeph"> .ptp-seek-to-bar</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .visualização múltipla</span> </td> 
   <td colname="col2"> <p>O estado do controle durante a visualização múltipla. </p> <p>Aplica-se ao seguinte: 
     <ul id="ul_A8AC653C30814AC49041F3B58A2106F4"> 
      <li id="li_0407167DA21647A8A6960DFE55A33F42"><span class="codeph"> .ptp-btn-fastforward</span> </li> 
      <li id="li_EA71CAF41CDC41DE859A85CE482BE97C"><span class="codeph"> .ptp-btn-share-video</span> </li> 
      <li id="li_F3A998C51A034C22A914EAEFF19FFEA7"><span class="codeph"> .ptp-btn-closed-caption</span> </li> 
      <li id="li_022F871ABC894C9BA879B3AF3D341202"><span class="codeph"> .ptp-btn-audio-track</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> .fullscreen-state</span> </td> 
   <td colname="col2"> <p>O reprodutor está no modo de tela cheia. </p> <p>Aplica-se ao seguinte: 
     <ul id="ul_B235C1D339F64B2FAC6BC72F03807616"> 
      <li id="li_6E050EE74C604FDAB4C9C0447F547A9D"><span class="codeph"> .ptp-control-bar </span> </li> 
      <li id="li_67D54B1A41764B2DA544479CDA1C901C"><span class="codeph"> .ptp-btn-fullscreen</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
