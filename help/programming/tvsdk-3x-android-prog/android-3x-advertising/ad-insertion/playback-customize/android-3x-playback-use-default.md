---
description: Você pode optar por usar comportamentos de anúncio padrão.
title: Usar o comportamento de reprodução padrão
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Usar o comportamento de reprodução padrão {#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de anúncio padrão.

1. Para usar comportamentos padrão, conclua uma das seguintes tarefas:

   * Se você implementar o seu próprio `AdvertisingFactory` classe, retornar nulo para `createAdPolicySelector`.

   * Se você não tiver uma implementação personalizada para o `AdvertisingFactory` classe, o TVSDK usa um seletor de política de anúncio padrão.

## Configurar reprodução personalizada {#set-up-customized-playback}

Você pode personalizar ou substituir comportamentos de anúncios.

Antes de personalizar ou substituir comportamentos de anúncios, registre a instância da política de anúncios com .
Para personalizar comportamentos de anúncios, siga um destes procedimentos:

* Implementar o `AdPolicySelector` e todos os seus métodos.

  Essa opção é recomendada se você precisar substituir **all** os comportamentos de anúncio padrão.

* Estenda o `DefaultAdPolicySelector` e fornecem implementações somente para os comportamentos que exigem personalização.

  Essa opção é recomendada se você precisar substituir apenas o **alguns** dos comportamentos padrão.

Para personalizar comportamentos de anúncios:

1. Implementar o `AdPolicySelector` e todos os seus métodos.
1. Atribua a instância de política a ser usada pelo TVSDK por meio da fábrica de publicidade.

   >[!NOTE]
   >
   >classe CustomContentFactory estende ContentFactory &amp;lbrace;
   >...
   >@Override
   >public AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >retornar novo CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rbrace;
   >...
   >&amp;rbrace;
   >// registrar a fábrica de conteúdo personalizado com o reprodutor de mídia
   >Configuração MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// essa configuração deverá ser passada posteriormente ao carregar >o recurso
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implemente suas personalizações.
