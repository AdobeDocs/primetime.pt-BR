---
description: Você pode optar por usar comportamentos de publicidade padrão.
title: Usar o comportamento de reprodução padrão
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '225'
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
Para personalizar os comportamentos do anúncio, siga um destes procedimentos:

* Implemente a interface `AdPolicySelector` e todos os seus métodos.

   Essa opção é recomendada se você precisar substituir **all** os comportamentos de publicidade padrão.

* Estenda a classe `DefaultAdPolicySelector` e forneça implementações somente para os comportamentos que exigem personalização.

   Essa opção é recomendada se você precisar substituir apenas **some** dos comportamentos padrão.

Para personalizar os comportamentos do anúncio:

1. Implemente a interface `AdPolicySelector` e todos os seus métodos.
1. Atribua a instância de política a ser usada pelo TVSDK por meio do setor de publicidade.

   >[!NOTE]
   >
   >Classe CustomContentFactory estende ContentFactory &amp;lbrace;
   >...
   >@Override
   >public AdPolicySelector retrieveAdPolicySelector>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >return new CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rbrace;
   >...
   >&amp;rbrace;
   >// registrar a fábrica de conteúdo personalizado no reprodutor de mídia
   >MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// essa configuração deve ser passada posteriormente durante o carregamento do recurso
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implemente suas personalizações.
