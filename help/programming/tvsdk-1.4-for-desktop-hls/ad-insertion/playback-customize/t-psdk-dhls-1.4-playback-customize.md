---
description: Você pode personalizar ou substituir comportamentos de publicidade.
seo-description: Você pode personalizar ou substituir comportamentos de publicidade.
seo-title: Configurar reprodução personalizada
title: Configurar reprodução personalizada
uuid: 479ca1b0-6b3f-42fa-85e1-31d707da8730
translation-type: tm+mt
source-git-commit: a21a5fcc819a7bec58ad36e118d04f462ec3fd92
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Configurar reprodução personalizada{#set-up-customized-playback}

Você pode personalizar ou substituir comportamentos de publicidade.

Antes de personalizar ou substituir comportamentos de publicidade, registre a instância da política de publicidade com .
Para personalizar os comportamentos de publicidade, execute um dos procedimentos a seguir:

* Implemente a interface `AdPolicySelector` e todos os seus métodos.

   Essa opção é recomendada se você precisar substituir **all** os comportamentos padrão do anúncio.

* Estenda a classe `DefaultAdPolicySelector` e forneça implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas **some** dos comportamentos padrão.

Para ambas as opções, conclua as seguintes tarefas:

1. Implemente seu próprio seletor de políticas de publicidade personalizado.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. Estenda a fábrica de conteúdo para usar o seletor de políticas de publicidade personalizadas.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       /** 
        * @inheritDoc 
        */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new CustomAdPolicySelector(item); 
       } 
   }
   ```

   ```
   psdkutils::PSDKSharedPointer<psdk::ContentFactory> factory; 
   psdkFactory->createDefaultContentFactory(&factory); 
   psdkutils::PSDKSharedPointer<psdk::AdPolicySelector> defaultAdPolicySelector; 
   factory->retrieveAdPolicySelector(item, &defaultAdPolicySelector);
   ```

1. Registre a nova fábrica de conteúdo a ser usada pelo TVSDK no fluxo de trabalho de publicidade.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Se a fábrica de conteúdo personalizado foi registrada para um fluxo específico por meio da classe `MediaPlayerItemConfig`, ela será apagada quando a instância `MediaPlayer` for desalocada. Seu aplicativo deve registrá-lo sempre que uma nova sessão de reprodução for criada.