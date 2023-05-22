---
description: Você pode ativar ou desativar os recursos sem passar pelo código usando a fábrica do gerente.
title: Ativando ou desativando recursos usando o ManagerFactory
exl-id: 4e288a6e-80e5-43c1-aba2-374723dd9957
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
