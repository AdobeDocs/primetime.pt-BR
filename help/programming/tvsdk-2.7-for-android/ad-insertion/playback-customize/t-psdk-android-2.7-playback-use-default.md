---
description: Você pode optar por usar comportamentos de publicidade padrão.
title: Usar o comportamento de reprodução padrão
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Usar o comportamento de reprodução padrão {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de publicidade padrão.

1. Para usar comportamentos padrão, conclua uma das seguintes tarefas:

   * Se você implementar sua própria classe `AdvertisingFactory`, retorne null para `createAdPolicySelector`.

   * Se você não tiver uma implementação personalizada para a classe `AdvertisingFactory`, o TVSDK usará um seletor de política de publicidade padrão.

## Configurar reprodução personalizada {#set-up-customized-playback}

Você pode personalizar ou substituir comportamentos de publicidade.

Antes de personalizar ou substituir comportamentos de anúncios, registre a instância da política de anúncios com TVSDK.

* Implemente a interface `AdPolicySelector` e todos os seus métodos.

   Essa opção é recomendada se você precisar substituir **all** os comportamentos de publicidade padrão.

* Estenda a classe `DefaultAdPolicySelector` e forneça implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas **some** dos comportamentos padrão.

Para personalizar os comportamentos do anúncio:

1. Implemente a interface `AdPolicySelector` e todos os seus métodos.
1. Atribua a instância de política a ser usada pelo TVSDK por meio do setor de publicidade.

   >[!NOTE]
   >
   >As políticas de anúncio personalizadas registradas no início da reprodução são apagadas quando a instância `MediaPlayer` é desalocada. O aplicativo deve registrar uma instância do seletor de políticas sempre que uma nova sessão de reprodução for criada.

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