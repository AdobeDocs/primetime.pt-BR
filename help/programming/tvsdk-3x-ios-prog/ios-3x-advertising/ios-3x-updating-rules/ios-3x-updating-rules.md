---
description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.
seo-title: Atualizar regras de seleção de anúncio
title: Atualizar regras de seleção de anúncio
uuid: b7d316ef-323e-4769-83d9-036422ae1707
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Visão geral {#update-ad-creative-selection-rules-overview}

Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.

Quando o player de vídeo faz uma solicitação para um servidor de publicidade, a resposta VAST/VMAP geralmente inclui vários anúncios (elementos `MediaFile`), cada um dos quais fornece um URL para uma versão diferente de codec de container. Em alguns casos, os anúncios criados na resposta VAST/VMAP fornecem uma taxa de bits diferente para o anúncio. Se você quiser especificar sua própria prioridade e regras de transformação para essas criações de anúncios, poderá fazê-lo no arquivo de configuração [!DNL AdobeTVSDKConfig.json].

>[!IMPORTANT]
>
>* Não altere o nome do arquivo de configuração do TVSDK. O nome deve permanecer [!DNL AdobeTVSDKConfig.json].
>* Você pode colocar esse arquivo em qualquer lugar acessível ao seu pacote.

>



Você pode especificar dois tipos de regras em [!DNL AdobeTVSDKConfig.json]: Regras *Priority* e *Normalizar* regras.

**[!UICONTROL Disabling Pre-Roll]**

Para desativar o pre-roll, é necessário alterar os geradores de oportunidade padrão para não fazer a chamada pré-roll. Por padrão, o TVSDK usa os seguintes geradores de oportunidade:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    result.push(new AdSignalingModeOpportunityGenerator()); 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
} 
```

Para desativar a pré-rolagem em fluxos ao vivo, isso deve ser alterado para incluir somente o SpliceOutOpportunityGenerator:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    if (preroll_enabled == true) { 
        result.push(new AdSignalingModeOpportunityGenerator()); 
    } 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
}
```
