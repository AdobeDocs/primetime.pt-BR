---
description: Você pode ativar ou desativar os recursos sem passar pelo código usando a fábrica do gerenciador.
title: Ativar ou desativar recursos usando o ManagerFactory
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Ativar ou desativar recursos usando o ManagerFactory{#turning-features-on-or-off-using-managerfactory}

Você pode ativar ou desativar os recursos sem passar pelo código usando a fábrica do gerenciador.

O argumento de ativação no exemplo abaixo determina se o recurso é usado ou não. Se for falso, o gerenciador de recursos será criado, mas fornecerá apenas a funcionalidade padrão do reprodutor, como se o gerenciador de recursos não tivesse sido criado. Se for verdadeiro, o gerenciador de recursos será criado, o recurso será ativado e o reprodutor de mídia aceitará a entrada do arquivo de configuração.

Por exemplo, no arquivo `com.adobe.primetime.reference.ui.player.PlayerFragment.java`:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**Documentação** da API:  [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)