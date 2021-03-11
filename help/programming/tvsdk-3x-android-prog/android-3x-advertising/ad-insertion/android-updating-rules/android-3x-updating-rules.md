---
description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Também é possível usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.
keywords: regras de seleção criativa; AdobeTVSDKConfig; prioridades criativas de anúncio; regras de transformação
title: Atualizar regras de seleção de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# Visão geral {#update-ad-creative-selection-rules-overview}

Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção de anúncio nas respostas VAST/VMAP. Também é possível usar esse arquivo de configuração para definir as regras de transformação do URL de origem para anúncios.

Quando o reprodutor de vídeo faz uma solicitação para um servidor de anúncios, a resposta VAST/VMAP geralmente inclui vários anúncios (elementos `MediaFile` ), cada um deles fornece um URL para uma versão diferente do codec de contêiner. Em alguns casos, os anúncios na resposta VAST/VMAP fornecem uma taxa de bits diferente para o anúncio. Se você quiser especificar sua própria prioridade e regras de transformação para esses anúncios, poderá fazer isso no arquivo de configuração [!DNL AdobeTVSDKConfig.json].

>[!IMPORTANT]
>
>* Não altere o nome do arquivo de configuração TVSDK. O nome deve permanecer [!DNL AdobeTVSDKConfig.json].
>* Esse arquivo deve ser colocado na pasta [!DNL assets/] do projeto.
>* Alterar as faixas de áudio quando o anúncio está sendo reproduzido não altera a faixa de áudio. Um reprodutor não deve permitir que os usuários alterem a faixa de áudio quando um anúncio está sendo reproduzido.

>



Você pode especificar dois tipos de regras em [!DNL AdobeTVSDKConfig.json]: Regras *Prioridade* e regras *Normalizar*.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

As regras de publicidade são especificadas usando um arquivo JSON. O formato do arquivo JSON permanece o mesmo em ambas as versões do TVSDK. No entanto, no TVSDK v3.0, o arquivo JSON de regras de publicidade deve ser hospedado em um local acessível por meio de um URL HTTP. O aplicativo pode usar uma instância de AuditudeSettings:

```
//TVSDK v3.0 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
