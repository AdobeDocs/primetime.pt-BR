---
description: Você pode personalizar ou substituir comportamentos de publicidade.
seo-description: Você pode personalizar ou substituir comportamentos de publicidade.
seo-title: Configurar reprodução personalizada
title: Configurar reprodução personalizada
uuid: 9cbf0bcf-7932-409e-a690-e79f284eaf74
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# Configurar reprodução personalizada {#cset-up-customized-playback}

Você pode personalizar ou sobrescrever o comportamento do anúncio, registrando a instância da política de publicidade no TVSDK.

Para personalizar os comportamentos de publicidade, execute um dos procedimentos a seguir:

* Implemente a interface `AdPolicySelector` e todos os seus métodos.
Essa opção é recomendada se você precisar substituir todos os comportamentos padrão de anúncio.

* Estende a classe `DefaultAdPolicySelector` e fornece implementações somente para os comportamentos que exigem
personalização.
Essa opção é recomendada se você precisar substituir apenas alguns dos comportamentos padrão.

Para ambas as opções, conclua as seguintes tarefas:

Para personalizar comportamentos de publicidade:

1. Implemente a interface AdPolicySelector e todos os seus métodos.

1. Atribua a instância de política a ser usada pelo TVSDK por meio da fábrica de publicidade.

>[!IMPORTANT]
>
>As políticas de publicidade personalizadas registradas no início da >reprodução são apagadas quando a instância do MediaPlayer é >desalocada. Seu aplicativo deve registrar uma instância de política >seletor sempre que uma nova sessão de reprodução é criada.

Por exemplo:

```
    class CustomContentFactory extends ContentFactory {
     ...
    @Override
    public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) {
    return new CustomAdPolicySelector(mediaPlayerItem);
    }
     ...
    }
    TVSDK 1.4 for Android Programmer's Guide 46
    // register the custom content factory with media player
    MediaPlayerItemConfig config = new MediaPlayerItemConfig();
    config.setAdvertisingFactory(new CustomContentFactory());
    // this config will should be later passed while loading the resource
    mediaPlayer.replaceCurrentResource(resource, config);
```

1. Implemente suas personalizações.