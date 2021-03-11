---
description: 'Você deve configurar as propriedades do servidor para refletir seu ambiente. Você pode fazer isso usando qualquer um dos seguintes '
title: Aplicar propriedades a ambientes de servidor
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Aplicar propriedades a ambientes do servidor{#apply-properties-to-server-environments}

Você deve configurar as propriedades do servidor para refletir seu ambiente. Você pode fazer isso usando qualquer um dos seguintes procedimentos:

* [!DNL flashaccess-i15n.properties] - Amostras incluídas em cada um dos  [!DNL .war] arquivos

* [!DNL AdobeInitial.properties] - Amostra localizada na  [!DNL /shared] pasta do DVD

   Você pode usar esse arquivo para substituir as propriedades definidas no arquivo WAR da seguinte maneira:

   1. Defina os valores de propriedade substitutos em [!DNL AdobeInitial.properties]
   1. Coloque [!DNL AdobeInitial.properties] no classpath.

   >[!NOTE]
   >
   >O Adobe recomenda que você use o arquivo [!DNL AdobeInitial.properties], já que isso permite atualizar os arquivos WAR do aplicativo sem arriscar a perda de qualquer configuração de propriedade anterior que você tenha feito no arquivo [!DNL flashaccess-i15n.properties].

* O mecanismo de propriedade Java System.

Você pode aplicar propriedades individuais a esses ambientes de servidor específicos:

* *Desenvolvimento*
* *Estágios*
* *Produção*

Com esse recurso, você pode usar o mesmo arquivo WAR para todos os ambientes de servidor. Para aplicar propriedades a ambientes específicos, anexe dois caracteres sublinhados (&#39; `__`&#39;) mais um dos seguintes códigos de ambiente à propriedade *name*:

    * `DEV`
    * `STAGE`
    * `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Por exemplo, para definir o nível de log para `INFO` para seus servidores de produção e de preparo, e para `DEBUG` para seu servidor de desenvolvimento:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

O servidor emprega esta ordem de pesquisa para propriedades:

1. `propertyname_environment` em  [!DNL AdobeInitial.properties]

1. `propertyname_environment` em  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` nas propriedades do Java System
1. `propertyname` em  [!DNL AdobeInitial.properties]

1. `propertyname` em  [!DNL flashaccess-15n.properties]

1. `propertyname` nas propriedades do Java System

>[!NOTE]
>
>Você deve especificar o nome do ambiente do servidor como uma propriedade do Java System ao iniciar o servidor. Por exemplo, ao iniciar o Tomcat com [!DNL catalina.bat], defina a variável de ambiente `CATALINA_OPTS` da seguinte maneira:
>-DENVIRONMENT_NAME=[ DEV | FASE | PROD ]
