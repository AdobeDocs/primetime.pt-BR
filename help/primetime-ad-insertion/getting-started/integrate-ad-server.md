---
title: Integre seu servidor de publicidade
description: Integração do servidor de publicidade
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Integre seu servidor de publicidade {#integrate-ad-server}

Para iniciar, você receberá um logon para acessar o console de Ad Insertion do Primetime, onde você configurará as regras que o Ad Insertion do Primetime usa para encaminhar solicitações de anúncios ao servidor de anúncios de sua escolha. O Primetime Ad Insertion suporta a maioria dos servidores de anúncios compatíveis com VAST ou VMAP.

>[!NOTE]
>
>[Página IAB VAST](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast)

## Suporte de macro {#macro-support}

O Ad Insertion do Primetime habilita as seguintes macros de servidor de publicidade para todos os fluxos:

* Interrupção de cache
* Contexto do aplicativo ou URL da página
* Duração disponível
* Ativo de vídeo atual

Se macros adicionais forem necessárias, entre em contato com o representante de suporte da Adobe Primetime.

## Recursos avançados {#advanced-features}

O Primetime Ad Insertion também apresenta decisões baseadas em regras que ativam recursos avançados. Isso pode ser importante se você quiser rotear anúncios para diferentes servidores de anúncios com base em direitos de inventário ou ativar o limite de frequência para anúncios individuais. Para obter mais informações, consulte [Recursos avançados](/help/primetime-ad-insertion/advanced-features/route-ads-based-on-rules.md).
