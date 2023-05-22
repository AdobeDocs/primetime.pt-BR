---
description: Você pode personalizar ou substituir comportamentos de anúncios.
title: Configurar reprodução personalizada
exl-id: 28c28589-9e94-40de-b921-1bffc0392c29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Configurar reprodução personalizada{#set-up-customized-playback}

Você pode personalizar ou substituir comportamentos de anúncios.

Antes de personalizar ou substituir comportamentos de anúncios, registre a instância da política de anúncios com .
Para personalizar comportamentos de anúncios, siga um destes procedimentos:

* Implementar o `AdPolicySelector` e todos os seus métodos.

   Essa opção é recomendada se você precisar substituir **all** os comportamentos de anúncio padrão.

* Estenda o `DefaultAdPolicySelector` e fornecem implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas o **alguns** dos comportamentos padrão.

Para ambas as opções, conclua as seguintes tarefas:

1. Implemente seu próprio seletor de políticas de anúncios personalizado.

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

1. Registre a nova fábrica de conteúdo a ser usada pelo TVSDK no fluxo de trabalho de publicidade.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Se a fábrica de conteúdo personalizado foi registrada para um fluxo específico por meio da `MediaPlayerItemConfig` será limpa quando a variável `MediaPlayer` instância desalocada. Seu aplicativo deve registrá-la sempre que uma nova sessão de reprodução for criada.
