---
title: Integrar seu servidor de publicidade
description: Integração do servidor de publicidade
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Integre seu servidor de publicidade {#integrate-ad-server}

Para o start, você receberá um login para acessar o console do Primetime Ad Insertion, onde você configurará regras que o Primetime Ad Insertion usa para encaminhar solicitações de anúncios ao servidor de anúncios de sua escolha. O Primetime Ad Insertion suporta a maioria dos servidores de anúncio compatíveis com VAST ou VMAP.

>[!NOTE]
>
>[Página VAST do IAB](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast)

## Suporte a macro {#macro-support}

O Primetime Ad Insertion habilita as seguintes macros de servidor de publicidade para todos os fluxos:

* Economia de cache
* Contexto do aplicativo ou url da página
* Duração disponível
* Ativo de vídeo atual

<!--For technical information regarding specific ad servers or ad macros, see [Supported ad servers and macros](supported-ad-servers-and-macros.md).-->

Se forem necessárias macros adicionais, entre em contato com seu representante de suporte da Adobe Primetime.

## Recursos avançados {#advanced-features}

O Primetime Ad Insertion também apresenta decisões baseadas em regras que habilitam recursos avançados. Isso pode ser importante se você quiser direcionar anúncios para diferentes servidores de anúncios com base em direitos de inventário ou habilitar o limite de frequência para anúncios individuais. <!--For more information, see [Advanced Features](route-ads-based-on-rules.md).-->
