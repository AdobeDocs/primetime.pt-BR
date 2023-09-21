---
description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção criativa de anúncios em respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para criações de anúncios.
keywords: regras de seleção criativa;AdobeTVSDKConfig;adicionar prioridades criativas;regras de transformação
title: Atualização das regras de seleção criativa de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Visão geral {#updating-ad-creative-selection-rules-overview}

Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção criativa de anúncios em respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para criações de anúncios.

Quando o reprodutor de vídeo faz uma solicitação a um servidor de anúncios, a resposta do VAST/VMAP geralmente inclui várias criações de anúncios ( `MediaFile` elementos ), cada um deles fornece um URL para uma versão diferente de codec de container. Em alguns casos, os anúncios criados na resposta VAST/VMAP fornecem uma taxa de bits diferente para o anúncio. Se quiser especificar sua própria prioridade e regras de transformação para esses anúncios, você pode fazê-lo no [!DNL AdobeTVSDKConfig.json] arquivo de configuração.

>[!IMPORTANT]
>
>* Não altere o nome do arquivo de configuração do TVSDK. O nome deve permanecer [!DNL AdobeTVSDKConfig.json].
>* Esse arquivo deve ser colocado no [!DNL assets/] pasta do seu projeto.
>

Você pode especificar dois tipos de regras em [!DNL AdobeTVSDKConfig.json]: *Prioridade* regras e *Normalizar* regras.

## Desativar o pré-lançamento {#disabling-preroll}

Para desativar o antes da exibição, será necessário alterar os geradores de oportunidade padrão para não fazer a chamada antes da exibição. Por padrão, o TVSDK usa os seguintes geradores de oportunidade:

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

Para desativar a pré-implantação em fluxos ao vivo, isso deve ser alterado para incluir apenas o SpliceOutOpportunityGenerator:

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
