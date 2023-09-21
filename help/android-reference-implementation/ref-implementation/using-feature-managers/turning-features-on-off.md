---
description: Você pode ativar ou desativar os recursos sem passar pelo código usando a fábrica do gerente.
title: Ativando ou desativando recursos usando o ManagerFactory
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Ativando ou desativando recursos usando o ManagerFactory{#turning-features-on-or-off-using-managerfactory}

Você pode ativar ou desativar os recursos sem passar pelo código usando a fábrica do gerente.

O argumento de ativação no exemplo abaixo determina se o recurso é usado ou não. Se for falso, o gerenciador de recursos será criado, mas fornecerá apenas a funcionalidade padrão para o reprodutor, como se o gerenciador de recursos não tivesse sido criado. Se for verdadeiro, o gerenciador de recursos será criado, o recurso será ativado e o reprodutor de mídia aceitará a entrada do arquivo de configuração.

Por exemplo, na variável `com.adobe.primetime.reference.ui.player.PlayerFragment.java` arquivo:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**Documentação da API**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
