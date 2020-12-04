---
description: 'Você deve configurar as propriedades do servidor para refletir seu ambiente. Você pode fazer isso usando qualquer uma das seguintes opções '
seo-description: 'Você deve configurar as propriedades do servidor para refletir seu ambiente. Você pode fazer isso usando qualquer uma das seguintes opções '
seo-title: Aplicar propriedades a ambientes de servidor
title: Aplicar propriedades a ambientes de servidor
uuid: a1ee0d6c-b5e7-4689-b7c8-b155176faf1c
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Aplicar propriedades a ambientes de servidor{#apply-properties-to-server-environments}

Você deve configurar as propriedades do servidor para refletir seu ambiente. Você pode fazer isso usando qualquer uma das seguintes opções:

* [!DNL flashaccess-i15n.properties] - Amostras incluídas em cada um dos  [!DNL .war] arquivos

* [!DNL AdobeInitial.properties] - Amostra localizada na  [!DNL /shared] pasta do DVD

   Você pode usar esse arquivo para substituir as propriedades definidas no arquivo WAR da seguinte forma:

   1. Defina os valores de propriedade substitutos em [!DNL AdobeInitial.properties]
   1. Coloque [!DNL AdobeInitial.properties] no classpath.

   >[!NOTE]
   >
   >O Adobe recomenda que você use o arquivo [!DNL AdobeInitial.properties], pois isso permite que você atualize os arquivos WAR do aplicativo sem arriscar a perda de qualquer configuração anterior de configuração de propriedade que você tenha feito no arquivo [!DNL flashaccess-i15n.properties].

* O mecanismo de propriedade do Java System.

É possível aplicar propriedades individuais a esses ambientes de servidor específicos:

* *Desenvolvimento*
* *Preparação*
* *Produção*

Com esse recurso, você pode usar o mesmo arquivo WAR para todos os ambientes do servidor. Para aplicar propriedades a ambientes específicos, acrescente dois caracteres sublinhados (&#39; `__`&#39;) mais um dos seguintes códigos de ambiente à propriedade *name*:

    * `DEV`
    * `PALCO`
    * `PROD&#39;

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Por exemplo, para definir o nível de log como `INFO` para seus servidores de produção e armazenamento temporário e como `DEBUG` para seu servidor de desenvolvimento:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

O servidor emprega esta ordem de pesquisa para propriedades:

1. `propertyname_environment` in  [!DNL AdobeInitial.properties]

1. `propertyname_environment` in  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` nas propriedades do Java System
1. `propertyname` in  [!DNL AdobeInitial.properties]

1. `propertyname` in  [!DNL flashaccess-15n.properties]

1. `propertyname` nas propriedades do Java System

>[!NOTE]
>
>É necessário especificar o nome do ambiente do servidor como uma propriedade do Java System ao iniciar o servidor. Por exemplo, ao iniciar o Tomcat com [!DNL catalina.bat], defina a variável de ambiente `CATALINA_OPTS` da seguinte maneira:
>-DENVIRONMENT_NAME=[ DEV | ETAPA | PROD ]
