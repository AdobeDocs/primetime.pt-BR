---
description: Você pode optar por usar comportamentos de publicidade padrão.
seo-description: Você pode optar por usar comportamentos de publicidade padrão.
seo-title: Usar o comportamento de reprodução padrão
title: Usar o comportamento de reprodução padrão
uuid: 20785251-eb2f-4cc0-b919-1a88c0b1c57c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Usar o comportamento de reprodução padrão {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de publicidade padrão.

1. Para usar comportamentos padrão, conclua uma das seguintes tarefas:

   * Se você implementar sua própria `AdvertisingFactory` classe, retorne null para `createAdPolicySelector`.

   * Se você não tiver uma implementação personalizada para a `AdvertisingFactory` classe, o TVSDK usará um seletor de política de publicidade padrão.

## Configurar reprodução personalizada {#set-up-customized-playback}

Você pode personalizar ou substituir comportamentos de publicidade.

Antes de personalizar ou substituir os comportamentos de publicidade, registre a instância da política de publicidade no TVSDK.

* Implemente a `AdPolicySelector` interface e todos os seus métodos.

   Essa opção é recomendada se você precisar substituir **todos** os comportamentos padrão de anúncio.

* Amplie a `DefaultAdPolicySelector` classe e forneça implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas **alguns** dos comportamentos padrão.

Para personalizar comportamentos de publicidade:

1. Implemente a `AdPolicySelector` interface e todos os seus métodos.
1. Atribua a instância de política a ser usada pelo TVSDK por meio da fábrica de publicidade.

   >[!NOTE]
   >
   >As políticas de anúncio personalizadas registradas no início da reprodução são apagadas quando a `MediaPlayer` instância é desalocada. Seu aplicativo deve registrar uma instância do seletor de política sempre que uma nova sessão de reprodução for criada.

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