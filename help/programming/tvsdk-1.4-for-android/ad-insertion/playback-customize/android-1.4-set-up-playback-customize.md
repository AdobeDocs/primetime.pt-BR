---
description: Você pode personalizar ou substituir comportamentos de publicidade.
title: Configurar reprodução personalizada
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 1%

---


# Configurar reprodução personalizada {#cset-up-customized-playback}

Você pode personalizar ou substituir o comportamento do anúncio, registrando a instância da política de anúncio com TVSDK.

Para personalizar os comportamentos do anúncio, siga um destes procedimentos:

* Implemente a interface `AdPolicySelector` e todos os seus métodos.
Essa opção é recomendada se você precisar substituir todos os comportamentos de publicidade padrão.

* Estender a classe `DefaultAdPolicySelector` e fornecer implementações somente para os comportamentos que exigem
personalização.
Essa opção é recomendada se você precisar substituir apenas alguns dos comportamentos padrão.

Para ambas as opções, conclua as seguintes tarefas:

Para personalizar os comportamentos do anúncio:

1. Implemente a interface AdPolicySelector e todos os seus métodos.

1. Atribua a instância de política a ser usada pelo TVSDK por meio do setor de publicidade.

>[!IMPORTANT]
>
>As políticas de anúncio personalizadas registradas no início da reprodução são apagadas quando a instância MediaPlayer é >desalocada. O aplicativo deve registrar uma instância de política > seletor sempre que uma nova sessão de reprodução for criada.

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