---
description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção criativa de anúncios em respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para criações de anúncios.
title: Atualização das regras de seleção criativa de anúncios
exl-id: 6664c120-2d4d-4cc0-8d9d-4bd8a66a5e88
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Visão geral {#updating-ad-creative-selection-rules}

Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção criativa de anúncios em respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para criações de anúncios.

Quando o reprodutor de vídeo faz uma solicitação a um servidor de anúncios, a resposta do VAST/VMAP geralmente inclui várias criações de anúncios ( `MediaFile` elementos ), cada um deles fornece um URL para uma versão diferente de codec de container. Em alguns casos, os anúncios criados na resposta VAST/VMAP fornecem uma taxa de bits diferente para o anúncio. Se quiser especificar sua própria prioridade e regras de transformação para esses anúncios, você pode fazê-lo no [!DNL AdobeTVSDKConfig.json] arquivo de configuração.

>[!IMPORTANT]
>
>* Não altere o nome do arquivo de configuração do TVSDK. O nome deve permanecer [!DNL AdobeTVSDKConfig.json].
>* Esse arquivo deve ser hospedado em sua rede de entrega de conteúdo (CDN).
>


Você pode especificar dois tipos de regras em [!DNL AdobeTVSDKConfig.json]: *Prioridade* regras e *Normalizar* regras.
