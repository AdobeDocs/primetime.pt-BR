---
description: Você pode configurar nomes de tag personalizados no TVSDK globalmente com a classe PTSDKConfig .
title: Métodos da classe Config para tags
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Métodos de classe de configuração para tags {#config-class-methods-for-tags}

Você pode configurar nomes de tag personalizados no TVSDK globalmente com a classe PTSDKConfig .

O TVSDK aplica a configuração global automaticamente a qualquer fluxo de mídia que não especifique uma configuração específica de fluxo.

`PTSDKConfig` expõe esses métodos para gerenciar as tags personalizadas:

| **Inscrever-se em tags personalizadas específicas** |  |
|---|---|
| `subscribedTags` | Recupera a lista atual de tags subscritas. |
| `setSubscribedTags` | Define a lista de tags assinadas que serão expostas ao aplicativo. |
| **Personalize as tags de publicidade usadas pelo detector de oportunidade padrão** |
| `adTags` | Recupera a lista atual de tags de anúncio. |
| `setAdTags` | Define a lista de tags de anúncio que serão usadas pelo gerador de oportunidade padrão. |


Lembre-se do seguinte:

* Os métodos setter não permitem que o parâmetro de tags contenha valores nulos.
* O nome da tag personalizada deve conter o prefixo # .

   Por exemplo, #EXT-X-ASSET é um nome de tag personalizada correto, mas EXT-X-ASSET está incorreto.
* Não é possível alterar a configuração após o carregamento do fluxo de mídia.