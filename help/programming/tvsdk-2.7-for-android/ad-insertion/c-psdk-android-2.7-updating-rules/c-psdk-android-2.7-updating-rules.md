---
description: Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção criativa de anúncios em respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para criações de anúncios.
keywords: regras de seleção criativa;AdobeTVSDKConfig;adicionar prioridades criativas;regras de transformação
title: Atualizar regras de seleção criativa de anúncios
exl-id: c11a7249-0036-4859-9e98-b0cac9ade5b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Visão geral {#update-ad-creative-selection-rules-overview}

Você pode usar o arquivo de configuração TVSDK (AdobeTVSDKConfig.json) para atualizar as prioridades para a seleção criativa de anúncios em respostas VAST/VMAP. Você também pode usar esse arquivo de configuração para definir as regras de transformação do URL de origem para criações de anúncios.

Quando o reprodutor de vídeo faz uma solicitação a um servidor de anúncios, a resposta do VAST/VMAP geralmente inclui várias criações de anúncios ( `MediaFile` elementos ), cada um deles fornece um URL para uma versão diferente de codec de container. Em alguns casos, os anúncios criados na resposta VAST/VMAP fornecem uma taxa de bits diferente para o anúncio. Se quiser especificar sua própria prioridade e regras de transformação para esses anúncios, você pode fazê-lo no [!DNL AdobeTVSDKConfig.json] arquivo de configuração.

>[!IMPORTANT]
>
>* Não altere o nome do arquivo de configuração do TVSDK. O nome deve permanecer [!DNL AdobeTVSDKConfig.json].
>* Esse arquivo deve ser colocado no [!DNL assets/] pasta do seu projeto.
>* Alterar faixas de áudio quando o anúncio está sendo reproduzido não altera a faixa de áudio. Um player não deve permitir que os usuários alterem a faixa de áudio quando um anúncio está sendo reproduzido.
>


Você pode especificar dois tipos de regras em [!DNL AdobeTVSDKConfig.json]: *Prioridade* regras e *Normalizar* regras.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

As Regras de publicidade são especificadas usando um arquivo JSON. O formato do arquivo JSON permanece o mesmo nas duas versões do TVSDK. No entanto, no TVSDK v2.5, o arquivo JSON de regras de anúncios deve ser hospedado em um local acessível por meio de um URL HTTP. O aplicativo pode usar uma instância do AuditudeSettings:

```
//TVSDK v2.5 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
