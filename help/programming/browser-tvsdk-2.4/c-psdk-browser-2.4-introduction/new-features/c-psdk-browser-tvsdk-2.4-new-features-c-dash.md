---
description: O TVSDK do navegador é compatível com vários recursos DASH que podem ser implementados para adicionar funcionalidade aos aplicativos de vídeo.
title: Recursos DASH compatíveis
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Recursos DASH compatíveis{#supported-dash-features}

O TVSDK do navegador é compatível com vários recursos DASH que podem ser implementados para adicionar funcionalidade aos aplicativos de vídeo.

* [Recursos de reprodução principal DASH](#dash-core-playback)
* [DASH Recursos avançados de reprodução](#dash-advanced-playback)
* [DASH Recursos de proteção de conteúdo](#dash-content-protection)
* [Recursos de inserção de anúncio do DASH Core](#dash-core-ad-insertion)
* [DASH Recursos avançados de inserção de anúncios](#dash-advanced-insertion-features)
* [Integrações DASH](#dash-integrations)

>[!TIP]
>
>Nas tabelas de matriz de recursos abaixo,  ![](assets/supported15.png)
>significa que o recurso é compatível com a versão atual.

Os seguintes recursos são compatíveis:

<!-- 

<table id="table_lrb_p2g_xx"> 
 <title>DASH integrations</title> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col6" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Category </th> 
    <th colname="col2" class="entry"> Content type </th> 
    <th colname="col3" class="entry"> Feature </th> 
    <th colname="col6" align="center" class="entry"> 
     <lines>
       HTML5 FF, IE, Chrome, Android Chrome
     </lines> </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_14D9248BD1D8410E83AD27DB4AB3B6ED" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_EFA853CB763446B3B37F2CF6BCC53EE1" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Billing </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_B3A4E5937CEC4052977C08767219BC2B" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Browserify </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_3330E81B86C84AD391AEBFDFE911A47F" /> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## Integrações DASH {#dash-integrations}

| Categoria | Tipo de conteúdo | Recurso | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Integrações | VOD + Ao vivo | Integração com o Adobe Analytics VHL | ![](assets/supported15.png) |
| Integrações | VOD + Ao vivo | Faturamento | ![](assets/supported15.png) |
| Integrações | VOD + Ao vivo | Browserify | ![](assets/supported15.png) |

## Recursos avançados de inserção de anúncio do DASH (CSAI) {#dash-advanced-insertion-features}

| Categoria | Tipo de conteúdo | Recurso | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD | Somente anúncio | Não suportado |
| Ad Insertion | VOD | Parâmetros de direcionamento | Somente VOD |
| Ad Insertion | VOD | Parâmetros personalizados | Somente VOD |
| Ad Insertion | VOD + Ao vivo | Política de publicidade personalizada | Não suportado |
| Ad Insertion | VOD + Ao vivo | Carregamento de anúncio lento | Não suportado |
| Ad Insertion | VOD | Anúncios de companhia, anúncios de banner e anúncios clicáveis | Não suportado |
| Ad Insertion | VOD | VPAID 2.0 | Não suportado |

## Recursos de inserção de anúncio principal DASH (CSAI) {#dash-core-ad-insertion}

| Categoria | Tipo de conteúdo | Recurso | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD + Ao vivo | Antes da exibição | Somente VOD |
| Ad Insertion | VOD + Ao vivo | Durante a exibição | Somente VOD |
| Ad Insertion | VOD + Ao vivo | Pós-rolagem | Somente VOD |
| Ad Insertion | FER VOD | Resolução e comportamentos do anúncio | Não suportado |
| Ad Insertion | VOD + Ao vivo | Política de publicidade padrão | Somente VOD |
| Ad Insertion | VOD + Ao vivo | VAST 2.0/3.0 | Somente VOD |
| Ad Insertion | VOD + Ao vivo | VMAP 1.0 | Somente VOD |
| Ad Insertion | VOD + Ao vivo | CRS v3.1 | Somente VOD |

## Recursos de proteção de conteúdo DASH {#dash-content-protection}

<table id="table_hrb_p2g_xx">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Categoria </th> 
   <th colname="col2" class="entry"> Tipo de conteúdo </th> 
   <th colname="col3" class="entry"> Recurso </th> 
   <th colname="col6" class="entry"> HTML5 FF, IE, Chrome, Android Chrome</th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Proteção de conteúdo </td> 
   <td colname="col2"> VOD + Ao vivo </td> 
   <td colname="col3"> AES-128 </td> 
   <td colname="col6"> Não suportado </td>
  </tr> 
  <tr> 
   <td colname="col1"> Proteção de conteúdo </td> 
   <td colname="col2"> VOD + Ao vivo </td> 
   <td colname="col3"> Amostra-AES </td> 
   <td colname="col6"> Não suportado </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Proteção de conteúdo </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3"> DRM </td> 
   <td colname="col6"> 
    <ul id="ul_irb_p2g_xx"> 
     <li id="li_C4643F2978BC4C8ABDB3E6C72C75A468">Widevine ativado 
      <ul id="ul_7047EA49AA3F40FE8F90E0ED6C028D83"> 
       <li id="li_B575735388D74D789D56BF373A470A6D">Cromo </li> 
       <li id="li_855146E4AC3A48E69B65F0022E1C0156">Firefox 47+ </li> 
       <li id="li_BC06B0A6EAAC4FC991C713775A8BB4DA">Chromecast </li> 
      </ul> </li> 
     <li id="li_D48B51C2208F423CB85D08886C2E1C66">PlayReady no Internet Explorer no Windows 8.1 e Edge </li> 
     <li id="li_2786AC19387241A296E015EE6FD07F2D">Acesso ao Adobe para Windows Firefox (somente vídeo) </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Recursos avançados de reprodução DASH {#dash-advanced-playback}

| Categoria | Tipo de conteúdo | Recurso | HTML5, FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Reprodução | VOD | Reprodução no deslocamento | ![](assets/supported15.png) |
| Reprodução | VOD | Reprodução somente de áudio | ![](assets/supported15.png) |
| Reprodução | VOD | Truque | ![](assets/supported15.png) |
| Reprodução | VOD | Truque suave Play | ![](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Análise de ID3 | Não suportado |
| Reprodução | VOD | Suporte a vários períodos | Somente VOD |
| Reprodução | VOD + Ao vivo | Fluxos tokenizados | Não suportado |
| Reprodução | VOD + Ao vivo | Faturamento | ![](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Browserify | ![](assets/supported15.png) |

## Principais recursos de reprodução do DASH {#dash-core-playback}

| Categoria | Tipo de conteúdo | Recurso | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Reprodução | VOD + Ao vivo | Reprodução geral (Reproduzir, Pausar, Buscar) | ![](assets/supported15.png) |
| Reprodução | FER VOD | Reprodução geral (Reproduzir, Pausar, Buscar) | Não suportado |
| Reprodução | VOD + Ao vivo | Taxa de bits adaptável | ![](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Legendas 608/708 | ![](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | WebVTT | Somente VOD |
| Reprodução | VOD + Ao vivo | Failover | Somente VOD |
| Reprodução | VOD + Ao vivo | Notificações de QoS e Player | ![](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Suporte para cabeçalhos de cookie | ![](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Definindo parâmetros de controle de buffer | ![](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Definir controles de taxa de bits adaptáveis | ![](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Tags personalizadas (EventStream) | Somente VOD (em linha) |
| Reprodução | VOD + Ao vivo | Áudio de associação tardia | Somente VOD |
| Reprodução | VOD + Ao vivo | redirecionamento 302 | Somente VOD |
