---
description: Você pode optar por usar comportamentos de publicidade padrão.
seo-description: Você pode optar por usar comportamentos de publicidade padrão.
seo-title: Usar o comportamento de reprodução padrão
title: Usar o comportamento de reprodução padrão
uuid: 36f76c42-4c6c-4620-9b47-ec97519a642a
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Usar o comportamento de reprodução padrão {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de publicidade padrão.

1. Para usar comportamentos padrão, conclua uma das seguintes tarefas:

   * Se você implementar sua própria classe `AdvertisingFactory`, retorne null para `createAdPolicySelector`.

   * Se você não tiver uma implementação personalizada para a classe `AdvertisingFactory`, o TVSDK usará um seletor de política de publicidade padrão.

## Configurar reprodução personalizada {#set-up-customized-playback}

Você pode personalizar ou substituir comportamentos de publicidade.

Antes de personalizar ou substituir comportamentos de publicidade, registre a instância da política de publicidade com .
Para personalizar os comportamentos de publicidade, execute um dos procedimentos a seguir:

* Implemente a interface `AdPolicySelector` e todos os seus métodos.

   Essa opção é recomendada se você precisar substituir **all** os comportamentos padrão do anúncio.

* Estenda a classe `DefaultAdPolicySelector` e forneça implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas **some** dos comportamentos padrão.

Para personalizar comportamentos de publicidade:

1. Implemente a interface `AdPolicySelector` e todos os seus métodos.
1. Atribua a instância de política a ser usada pelo TVSDK por meio da fábrica de publicidade.

   >[!NOTE]
   >
   >class CustomContentFactory estende ContentFactory &amp;lbrace;
   >...
   >@Substituir
   >public AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >retornar novo CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rbrace;
   >...
   >&amp;rbrace;
   >// registrar a fábrica de conteúdo personalizado no player de mídia
   >MediaPlayerItemConfig config = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// esta configuração será transmitida posteriormente ao carregar > o recurso
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implemente suas personalizações.
