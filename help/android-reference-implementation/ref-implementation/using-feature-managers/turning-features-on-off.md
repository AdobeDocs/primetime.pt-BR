---
description: Você pode ativar ou desativar recursos sem passar pelo código usando a fábrica do gerenciador.
seo-description: Você pode ativar ou desativar recursos sem passar pelo código usando a fábrica do gerenciador.
seo-title: Ativar ou desativar recursos usando o ManagerFactory
title: Ativar ou desativar recursos usando o ManagerFactory
uuid: 385c2707-95f7-4628-8d25-67731151cb6a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Ativar ou desativar recursos usando o ManagerFactory{#turning-features-on-or-off-using-managerfactory}

Você pode ativar ou desativar recursos sem passar pelo código usando a fábrica do gerenciador.

O argumento de ativação no exemplo abaixo determina se o recurso é usado ou não. Se for falso, o gerenciador de recursos será criado, mas fornecerá apenas a funcionalidade padrão para o player, como se o gerenciador de recursos não tivesse sido criado. Se for verdadeiro, o gerenciador de recursos será criado, o recurso será ativado e o player de mídia aceitará a entrada do arquivo de configuração.

Por exemplo, no `com.adobe.primetime.reference.ui.player.PlayerFragment.java` arquivo:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**Documentação** da API: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)