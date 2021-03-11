---
description: O TVSDK do navegador é compatível com vários recursos de HLS que você pode implementar para adicionar funcionalidade a seus aplicativos de vídeo.
title: Recursos HLS suportados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# Recursos HLS suportados {#supported-hls-features}

O TVSDK do navegador é compatível com vários recursos de HLS que você pode implementar para adicionar funcionalidade a seus aplicativos de vídeo.

* [Reprodução principal do HLS](#hls-core-playback)
* [Recursos de reprodução avançada HLS](#hls-advanced-playback)
* [Recursos de proteção de conteúdo do HLS](#hls-content-protection)
* [Recursos de inserção de anúncios do HLS Core](#hls-core-ad-insertion)
* [Recursos avançados de inserção de anúncios do HLS](#hls-advanced-ad-insertion)
* [Integrações de HLS](#hls-integrations)

>[!TIP]
>
>Nas tabelas de matriz de recursos abaixo, ![ícone suportado](assets/supported15.png) significa que o recurso é suportado na versão atual.

>[!TIP]
>
>Na coluna Safari, &quot;Limitação da plataforma&quot; significa que o caso de uso não é suportado, pois essa plataforma não permite a implementação do suporte para ela. No caso de uma inserção, use SSAI. Se houver limitações de reprodução importantes para você, force o fallback para o Flash no Safari até que a plataforma suporte o caso de uso de inserção de anúncio.

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

Os seguintes recursos são compatíveis:

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

## Integrações de HLS {#hls-integrations}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Integrações | VOD + Ao vivo | Integração do Adobe Analytics VHL | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |

## Recursos avançados de inserção de anúncio (CSAI) do HLS {#hls-advanced-ad-insertion}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | Somente publicidade | Não suportado | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | Parâmetros de direcionamento | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | Política de anúncio personalizada | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Ao vivo | Carregamento lento de anúncio | ![ícone suportado](assets/supported15.png) | Não suportado | Limitação da plataforma |
| Ad Insertion | VOD | Anúncios complementares, anúncios em banners e anúncios clicáveis | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Recursos de inserção de anúncio do núcleo do HLS (CSAI) {#hls-core-ad-insertion}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Ao vivo | Antes da exibição | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | Meio da exibição | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Ao vivo | Pós-lançamento | Somente VOD | Somente VOD | Somente VOD |
| Ad Insertion | FER VOD | Resolução e comportamento do anúncio | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Ao vivo | Política de publicidade padrão | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Ao vivo | VAST 2.0/3.0 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | VMAP 1.0 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | CRS v3.1 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |

## Recursos de proteção de conteúdo HLS {#hls-content-protection}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Proteção de conteúdo | VOD + Ao vivo | AES-128 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Proteção de conteúdo | VOD + Ao vivo | AES de exemplo | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Proteção de conteúdo | VOD | DRM | Acesso ao Adobe | Não suportado | FairPlay |

## Recursos de reprodução avançada HLS {#hls-advanced-playback}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD | Reprodução no offset | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD | Reprodução somente de áudio | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD | Trick Play | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD | Peça de truque suave | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Análise do ID3 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Não suportado |
| Reprodução | VOD + Ao vivo | Suporte ao marcador de descontinuidade | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Fluxos Tokenized | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Faturamento | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Procurar | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |

## Reprodução principal HLS {#hls-core-playback}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD + Ao vivo | Reprodução geral (Reproduzir, Pausar, Buscar) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | FER VOD | Reprodução geral (Reproduzir, Pausar, Buscar) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Taxa de bits adaptável | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | 608/708 legendas | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | WebVTT | ![ícone suportado](assets/supported15.png) | Somente VOD | Somente VOD |
| Reprodução | VOD + Ao vivo | Failover Manifest | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Failover avançado | ![ícone suportado](assets/supported15.png) | Somente VOD | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Notificações de QoS e player | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Suporte a QoS limitado |
| Reprodução | VOD + Ao vivo | Suporte para cabeçalhos de cookies | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Definindo parâmetros de controle de buffer | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Definir controles adaptáveis da taxa de bits | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Tags personalizadas | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Áudio de ligação tardia | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | 302 redirecionamento | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |