---
description: Você pode personalizar ou substituir comportamentos de anúncios.
title: Configurar reprodução personalizada
exl-id: aaa4d1c2-c425-4a2e-8377-0a3072f3fb18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Configurar reprodução personalizada {#cset-up-customized-playback}

Você pode personalizar ou substituir o comportamento do anúncio registrando a instância da política de anúncios com o TVSDK.

Para personalizar comportamentos de anúncios, siga um destes procedimentos:

* Implementar o `AdPolicySelector` e todos os seus métodos.
Essa opção é recomendada se você precisar substituir todos os comportamentos de anúncio padrão.

* Estenda o `DefaultAdPolicySelector` e fornecem implementações somente para os comportamentos que exigem personalização.
Essa opção é recomendada se você precisar substituir apenas alguns dos comportamentos padrão.

Para ambas as opções, conclua as seguintes tarefas:

Para personalizar comportamentos de anúncios:

1. Implemente a interface AdPolicySelector e todos os seus métodos.

1. Atribua a instância de política a ser usada pelo TVSDK por meio da fábrica de publicidade.

>[!IMPORTANT]
>
>As políticas de anúncios personalizados registradas no início da reprodução são apagadas quando a ocorrência do MediaPlayer é desalocada. Seu aplicativo deve registrar uma ocorrência de seletor de política sempre que uma nova sessão de reprodução é criada.

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
