---
description: Você pode personalizar ou substituir comportamentos de publicidade.
title: Configurar reprodução personalizada
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Configurar reprodução personalizada{#set-up-customized-playback}

Você pode personalizar ou substituir comportamentos de publicidade.

Antes de personalizar ou substituir comportamentos de publicidade, registre a instância da política de publicidade com .
Para personalizar os comportamentos do anúncio, siga um destes procedimentos:

* Implemente a interface `AdPolicySelector` e todos os seus métodos.

   Essa opção é recomendada se você precisar substituir **all** os comportamentos de publicidade padrão.

* Estenda a classe `DefaultAdPolicySelector` e forneça implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas **some** dos comportamentos padrão.

Para ambas as opções, conclua as seguintes tarefas:

1. Implemente seu próprio seletor de política de anúncio personalizado.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. Estenda a fábrica de conteúdo para usar o seletor de política de anúncio personalizado.

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

1. Registre a nova fábrica de conteúdo que será usada pelo TVSDK no fluxo de trabalho de publicidade.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Se a fábrica de conteúdo personalizado foi registrada para um fluxo específico por meio da classe `MediaPlayerItemConfig`, ela será apagada quando a instância `MediaPlayer` for desalocada. O aplicativo deve registrá-lo sempre que uma nova sessão de reprodução for criada.