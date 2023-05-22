---
description: Você pode optar por usar comportamentos de anúncio padrão.
title: Usar o comportamento de reprodução padrão
exl-id: eb4ce0b4-9dfd-4de8-8cbf-8aba093a5ddd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Usar o comportamento de reprodução padrão  {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de anúncio padrão.

1. Para usar comportamentos padrão, conclua uma das seguintes tarefas:

   * Se você implementar o seu próprio `AdvertisingFactory` classe, retornar nulo para `createAdPolicySelector`.

   * Se você não tiver uma implementação personalizada para o `AdvertisingFactory` classe, o TVSDK usa um seletor de política de anúncio padrão.

## Configurar reprodução personalizada {#set-up-customized-playback}

Você pode personalizar ou substituir comportamentos de anúncios.

Antes de personalizar ou substituir comportamentos de anúncios, registre a instância da política de anúncios com o TVSDK.

* Implementar o `AdPolicySelector` e todos os seus métodos.

   Essa opção é recomendada se você precisar substituir **all** os comportamentos de anúncio padrão.

* Estenda o `DefaultAdPolicySelector` e fornecem implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas o **alguns** dos comportamentos padrão.

Para personalizar comportamentos de anúncios:

1. Implementar o `AdPolicySelector` e todos os seus métodos.
1. Atribua a instância de política a ser usada pelo TVSDK por meio da fábrica de publicidade.

   >[!NOTE]
   >
   >As políticas de anúncios personalizados registradas no início da reprodução são apagadas quando a variável `MediaPlayer` instância desalocada. Seu aplicativo deve registrar uma instância do seletor de políticas sempre que uma nova sessão de reprodução for criada.

   Por exemplo:

   ```java
   class CustomContentFactory extends ContentFactory { 
       ... 
       @Override 
       public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           return new CustomAdPolicySelector(mediaPlayerItem); 
       } 
       ... 
   } 
   
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new CustomContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config);
   ```

1. Implemente suas personalizações.
