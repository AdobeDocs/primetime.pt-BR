---
description: O TVSDK do navegador é compatível com vários recursos HLS que você pode implementar para adicionar funcionalidade a seus aplicativos de vídeo.
title: Recursos HLS compatíveis
exl-id: 111a6683-fb5c-4f0a-8665-5b1aab77056c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Recursos HLS compatíveis {#supported-hls-features}

O TVSDK do navegador é compatível com vários recursos HLS que você pode implementar para adicionar funcionalidade a seus aplicativos de vídeo.

* [Reprodução principal HLS](#hls-core-playback)
* [Recursos avançados de reprodução HLS](#hls-advanced-playback)
* [Recursos de proteção de conteúdo HLS](#hls-content-protection)
* [Recursos principais de inserção de anúncio do HLS](#hls-core-ad-insertion)
* [Recursos avançados de inserção de anúncios do HLS](#hls-advanced-ad-insertion)
* [Integrações HLS](#hls-integrations)

>[!TIP]
>
>Nas tabelas de matriz de recursos abaixo, ![ícone suportado](assets/supported15.png) significa que o recurso é compatível com a versão atual.

>[!TIP]
>
>Na coluna do Safari, &quot;Limitação de plataforma&quot; significa que o caso de uso não é compatível, pois essa plataforma não permite a implementação do suporte para ele. No caso de uma inserção, use SSAI. Se houver limitações de reprodução importantes para você, force o fallback para o Flash no Safari até que a plataforma suporte o caso de uso de inserção de anúncio.

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

## Integrações HLS {#hls-integrations}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Integrações | VOD + Ao vivo | Integração com o Adobe Analytics VHL | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |

## Recursos avançados de inserção de anúncios HLS (CSAI) {#hls-advanced-ad-insertion}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | Somente anúncio | Não suportado | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | Parâmetros de direcionamento | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | Política de publicidade personalizada | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Ao vivo | Carregamento de anúncio lento | ![ícone suportado](assets/supported15.png) | Não suportado | Limitação da plataforma |
| Ad Insertion | VOD | Anúncios complementares, anúncios de banner e anúncios clicáveis | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Recursos principais de inserção de anúncio do HLS (CSAI) {#hls-core-ad-insertion}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Ao vivo | Antes da exibição | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | Durante a exibição | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Ao vivo | Pós-rolagem | Somente VOD | Somente VOD | Somente VOD |
| Ad Insertion | FER VOD | Resolução e comportamentos do anúncio | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Ao vivo | Política de publicidade padrão | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Ad Insertion | VOD + Ao vivo | VAST 2.0/3.0 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | VMAP 1.0 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Ad Insertion | VOD + Ao vivo | CRS v3.1 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |

## Recursos de proteção de conteúdo HLS {#hls-content-protection}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Proteção de conteúdo | VOD + Ao vivo | AES-128 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Proteção de conteúdo | VOD + Ao vivo | Amostra-AES | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Proteção de conteúdo | VOD | DRM | Acesso ao Adobe | Não suportado | FairPlay |

## Recursos avançados de reprodução HLS {#hls-advanced-playback}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD | Reprodução no deslocamento | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD | Reprodução somente de áudio | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD | Truque | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD | Truque suave | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Análise de ID3 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Não suportado |
| Reprodução | VOD + Ao vivo | Suporte a marcador de descontinuidade | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Fluxos tokenizados | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Faturamento | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Browserify | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |

## Reprodução principal HLS {#hls-core-playback}

| Categoria | Tipo de conteúdo | Recurso | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reprodução | VOD + Ao vivo | Reprodução geral (Reproduzir, Pausar, Buscar) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | FER VOD | Reprodução geral (Reproduzir, Pausar, Buscar) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Taxa de bits adaptável | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Legendas 608/708 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | WebVTT | ![ícone suportado](assets/supported15.png) | Somente VOD | Somente VOD |
| Reprodução | VOD + Ao vivo | Failover do manifesto | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) |
| Reprodução | VOD + Ao vivo | Failover avançado | ![ícone suportado](assets/supported15.png) | Somente VOD | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Notificações de QoS e player | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Suporte limitado a QoS |
| Reprodução | VOD + Ao vivo | Suporte para cabeçalhos de cookie | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Definindo parâmetros de controle de buffer | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Definir controles de taxa de bits adaptáveis | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Tags personalizadas | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | Áudio de associação tardia | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
| Reprodução | VOD + Ao vivo | redirecionamento 302 | ![ícone suportado](assets/supported15.png) | ![ícone suportado](assets/supported15.png) | Limitação da plataforma |
