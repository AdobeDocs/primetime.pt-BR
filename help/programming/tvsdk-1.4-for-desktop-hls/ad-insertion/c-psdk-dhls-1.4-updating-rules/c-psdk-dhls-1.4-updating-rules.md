---
description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Também é possível usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.
title: Atualização das regras de seleção de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Visão geral {#updating-ad-creative-selection-rules}

Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Também é possível usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.

Quando o reprodutor de vídeo faz uma solicitação para um servidor de anúncios, a resposta VAST/VMAP geralmente inclui vários anúncios (elementos `MediaFile` ), cada um deles fornece um URL para uma versão diferente do codec de contêiner. Em alguns casos, os anúncios na resposta VAST/VMAP fornecem uma taxa de bits diferente para o anúncio. Se você quiser especificar sua própria prioridade e regras de transformação para esses anúncios, poderá fazer isso no arquivo de configuração [!DNL AdobeTVSDKConfig.json].

>[!IMPORTANT]
>
>* Não altere o nome do arquivo de configuração TVSDK. O nome deve permanecer [!DNL AdobeTVSDKConfig.json].
>* Esse arquivo deve ser hospedado em sua rede de entrega de conteúdo (CDN).

>



Você pode especificar dois tipos de regras em [!DNL AdobeTVSDKConfig.json]: Regras *Prioridade* e regras *Normalizar*.
