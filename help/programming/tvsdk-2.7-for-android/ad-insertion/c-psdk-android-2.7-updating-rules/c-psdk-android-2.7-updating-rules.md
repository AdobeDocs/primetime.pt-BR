---
description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.
seo-title: Atualizar regras de seleção de anúncio
title: Atualizar regras de seleção de anúncio
uuid: fddc5593-db40-4b03-bd7e-4b5fe5b6f650
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Visão geral {#update-ad-creative-selection-rules-overview}

Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.

Quando o player de vídeo faz uma solicitação para um servidor de publicidade, a resposta VAST/VMAP geralmente inclui vários anúncios (elementos `MediaFile`), cada um dos quais fornece um URL para uma versão diferente de codec de container. Em alguns casos, os anúncios criados na resposta VAST/VMAP fornecem uma taxa de bits diferente para o anúncio. Se você quiser especificar sua própria prioridade e regras de transformação para essas criações de anúncios, poderá fazê-lo no arquivo de configuração [!DNL AdobeTVSDKConfig.json].

>[!IMPORTANT]
>
>* Não altere o nome do arquivo de configuração do TVSDK. O nome deve permanecer [!DNL AdobeTVSDKConfig.json].
>* Esse arquivo deve ser colocado na pasta [!DNL assets/] do seu projeto.
>* Alterar as faixas de áudio quando o anúncio está sendo reproduzido não altera a faixa de áudio. Um player não deve permitir que os usuários alterem a faixa de áudio quando um anúncio está sendo reproduzido.

>



Você pode especificar dois tipos de regras em [!DNL AdobeTVSDKConfig.json]: Regras *Priority* e *Normalizar* regras.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

As regras de publicidade são especificadas usando um arquivo JSON. O formato do arquivo JSON permanece o mesmo em ambas as versões do TVSDK. No entanto, no TVSDK v2.5, o arquivo JSON das regras do anúncio deve ser hospedado em um local acessível por meio de um URL HTTP. O aplicativo pode usar uma instância de AuditudeSettings:

```
//TVSDK v2.5 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```

