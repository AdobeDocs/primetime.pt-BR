---
description: Você pode optar por usar comportamentos de publicidade padrão.
seo-description: Você pode optar por usar comportamentos de publicidade padrão.
seo-title: Usar o comportamento de reprodução padrão
title: Usar o comportamento de reprodução padrão
uuid: 36f76c42-4c6c-4620-9b47-ec97519a642a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Usar o comportamento de reprodução padrão {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de publicidade padrão.

1. Para usar comportamentos padrão, conclua uma das seguintes tarefas:

   * Se você implementar sua própria `AdvertisingFactory` classe, retorne null para `createAdPolicySelector`.

   * Se você não tiver uma implementação personalizada para a `AdvertisingFactory` classe, o TVSDK usará um seletor de política de publicidade padrão.

## Configurar reprodução personalizada {#set-up-customized-playback}

Você pode personalizar ou substituir comportamentos de publicidade.

Antes de personalizar ou substituir comportamentos de publicidade, registre a instância da política de publicidade com .
Para personalizar os comportamentos de publicidade, execute um dos procedimentos a seguir:

* Implemente a `AdPolicySelector` interface e todos os seus métodos.

   Essa opção é recomendada se você precisar substituir **todos** os comportamentos padrão de anúncio.

* Amplie a `DefaultAdPolicySelector` classe e forneça implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas **alguns** dos comportamentos padrão.

Para personalizar comportamentos de publicidade:

1. Implemente a `AdPolicySelector` interface e todos os seus métodos.
1. Atribua a instância de política a ser usada pelo TVSDK por meio da fábrica de publicidade.

>[!NOTE]
>class CustomContentFactory estende ContentFactory {
>...
>@Substituir
>public AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) {
>retornar novo CustomAdPolicySelector(mediaPlayerItem);
>}
>...
>}
>// registrar a fábrica de conteúdo personalizado no player de mídia
>MediaPlayerItemConfig config = new MediaPlayerItemConfig();
>config.setAdvertisingFactory(new CustomContentFactory());
>// esta configuração será transmitida posteriormente ao carregar > o recurso
>mediaPlayer.replaceCurrentResource(resource, config);

1. Implemente suas personalizações.