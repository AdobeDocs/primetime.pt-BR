---
description: O TVSDK do navegador suporta vários recursos HLS que você pode implementar para adicionar funcionalidade aos seus aplicativos de vídeo.
seo-description: O TVSDK do navegador suporta vários recursos HLS que você pode implementar para adicionar funcionalidade aos seus aplicativos de vídeo.
seo-title: Recursos HLS suportados
title: Recursos HLS suportados
uuid: 033d81f8-cea4-4687-b2fb-1524d9164d39
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---


# Recursos HLS suportados {#supported-hls-features}

O TVSDK do navegador suporta vários recursos HLS que você pode implementar para adicionar funcionalidade aos seus aplicativos de vídeo.

* [Reprodução principal HLS](#hls-core-playback)
* [Recursos de reprodução avançada HLS](#hls-advanced-playback)
* [Recursos de proteção de conteúdo HLS](#hls-content-protection)
* [Recursos de inserção de anúncio do HLS Core](#hls-core-ad-insertion)
* [Recursos avançados de inserção de anúncios HLS](#hls-advanced-ad-insertion)
* [Integrações HLS](#hls-integrations)

>[!TIP]
>
>Nas tabelas de matriz de recursos abaixo, ![ícone suportado](assets/supported15.png) significa que o recurso é suportado na versão atual.

>[!TIP]
>
>Na coluna Safari, &quot;Limitação da plataforma&quot; significa que o caso de uso não é suportado porque essa plataforma não permite a implementação do suporte para ela. No caso de uma inserção, utilize SSAI. Se houver limitações de reprodução importantes para você, force o fallback para o Flash no Safari até que a plataforma suporte o caso de uso de inserção de anúncio.

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

Os seguintes recursos são suportados:

<!-- 

Removed Nielsen row 
<table id="table_D9E2D82992554905A0A551CC71AFA189"> 
 <title>HLS integrations</title> 
 <tgroup cols="6"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col4" colwidth="*" /> 
  <colspec colnum="5" colname="col5" colwidth="*" /> 
  <colspec colnum="6" colname="col7" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" morerows="1" class="entry"> Category </th> 
    <th colname="col2" morerows="1" class="entry"> Content type </th> 
    <th colname="col3" morerows="1" class="entry"> Feature </th> 
    <th colname="col4" morerows="1" class="entry"> Flash </th> 
    <th namest="col5" nameend="col7" class="entry"> HTML5 </th> 
   </tr> 
   <tr> 
    <th colname="col5" class="entry"> FF, IE, Chrome, Android Chrome </th> 
    <th colname="col7" class="entry"> Safari, iOS Safari </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## Integrações HLS {#hls-integrations}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Integrações | VOD + Live | Integração Adobe Analytics VHL | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |

## Recursos avançados de inserção de anúncios (CSAI) HLS {#hls-advanced-ad-insertion}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | Somente publicidade | Não suportado | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Live | Parâmetros de definição de metas | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Live | Política de anúncio personalizada | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Live | Carregamento de anúncio ocioso | ![ícone suportado](assets/supported15.png) | Não suportado | Limitação da plataforma |
| Ad Insertion | VOD | Anúncios complementares, anúncios em banners e anúncios clicáveis | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Recursos de inserção de anúncio do núcleo do HLS (CSAI) {#hls-core-ad-insertion}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Live | Pré-lançamento | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Live | Meia rolagem | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Live | Pós-rolagem | Somente VOD | Somente VOD | Somente VOD |
| Ad Insertion | FER VOD | Resolução e comportamento do anúncio | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Live | Política de publicidade padrão | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Live | VAST 2.0/3.0 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Live | VMAP 1.0 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Live | CRS v3.1 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |

## Recursos de proteção de conteúdo HLS {#hls-content-protection}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Proteção de conteúdo | VOD + Live | AES-128 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Proteção de conteúdo | VOD + Live | AES de amostra | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Proteção de conteúdo | VOD | DRM | Acesso ao Adobe | Não suportado | FairPlay |

## Recursos de reprodução avançada HLS {#hls-advanced-playback}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD | Reprodução em offset | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD | Reprodução somente de áudio | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD | peça | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD | Brincadeira suave | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Live | Análise de ID3 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Não suportado |
| Reprodução | VOD + Live | Suporte ao marcador de descontinuidade | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Live | Fluxos Tokenized | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Live | Cobrança | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Live | Procurar | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |

## Reprodução principal HLS {#hls-core-playback}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD + Live | Reprodução geral (Reproduzir, Pausar, Buscar) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | FER VOD | Reprodução geral (Reproduzir, Pausar, Buscar) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Live | Taxa de bits adaptável | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Live | Legendas 608/708 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Live | WebVTT | ![ícone suportado](assets/supported15.png) | Somente VOD | Somente VOD |
| Reprodução | VOD + Live | Failover Manifest | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Live | Failover avançado | ![ícone suportado](assets/supported15.png) | Somente VOD | Limitação da plataforma |
| Reprodução | VOD + Live | Notificações de QoS e player | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Suporte a QoS limitado |
| Reprodução | VOD + Live | Suporte para cabeçalhos de cookies | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Live | Definição de parâmetros de controle de buffer | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Live | Definir controles adaptáveis de taxa de bits | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Live | Tags personalizadas | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Live | Áudio de ligação tardia | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Live | Redirecionamento 302 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |