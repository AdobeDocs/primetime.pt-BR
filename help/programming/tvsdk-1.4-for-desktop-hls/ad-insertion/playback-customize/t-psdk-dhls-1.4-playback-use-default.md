---
description: Você pode optar por usar comportamentos de publicidade padrão.
seo-description: Você pode optar por usar comportamentos de publicidade padrão.
seo-title: Usar o comportamento de reprodução padrão
title: Usar o comportamento de reprodução padrão
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Usar o comportamento de reprodução padrão{#use-the-default-playback-behavior}

Você pode optar por usar comportamentos de publicidade padrão.

Para usar comportamentos padrão:

    * Se você implementar sua própria classe &quot;ContentFactory&quot;, retorne uma nova instância de &quot;DefaultAdPolicySelector&quot; na implementação de &quot;doRetrieveAdPolicySelector&quot;.
    
    &quot;Classe
    pública CustomContentFactory estende ContentFactory {
    
    /...
    // seu código personalizado para classes
    //...
    
    /**
    * @hereitDoc
    */
    override protected
    functionRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector {
    return new DefaultAdPolicySelector(item);
    }
    &quot;
    
    
    * Se você não tiver uma implementação personalizada para a classe &quot;ContentFactory&quot;, TVSDK O DK usa &quot;DefaultAdPolicySelector&quot;.