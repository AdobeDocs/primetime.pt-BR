---
description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.
seo-description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.
seo-title: Atualização das regras de seleção de anúncio
title: Atualização das regras de seleção de anúncio
uuid: 9eb4ccc2-425f-4c01-a095-f2043df4e25c
translation-type: tm+mt
source-git-commit: 6837c753b2f031b024ff510cda670340f346c4e1

---


# Visão geral {#updating-ad-creative-selection-rules}

Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.

Quando o player de vídeo faz uma solicitação para um servidor de publicidade, a resposta VAST/VMAP geralmente inclui vários anúncios ( `MediaFile` elementos), cada um deles fornecendo um URL para uma versão diferente do codec do contêiner. Em alguns casos, os anúncios criados na resposta VAST/VMAP fornecem uma taxa de bits diferente para o anúncio. Se você quiser especificar sua própria prioridade e regras de transformação para essas criações de anúncios, poderá fazer isso no arquivo de [!DNL AdobeTVSDKConfig.json] configuração.

>[!IMPORTANT]
>
>* Não altere o nome do arquivo de configuração do TVSDK. O nome deve permanecer [!DNL AdobeTVSDKConfig.json].
>* Esse arquivo deve ser hospedado em sua rede de entrega de conteúdo (CDN).
>



Você pode especificar dois tipos de regras em [!DNL AdobeTVSDKConfig.json]: Regras de *prioridade* e regras de *normalização* .
