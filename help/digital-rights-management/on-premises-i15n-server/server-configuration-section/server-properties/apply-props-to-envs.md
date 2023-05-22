---
description: Você deve configurar as propriedades do servidor para refletir seu ambiente. Você pode fazer isso usando qualquer um dos seguintes
title: Aplicar propriedades a ambientes de servidor
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Aplicar propriedades a ambientes de servidor{#apply-properties-to-server-environments}

Você deve configurar as propriedades do servidor para refletir seu ambiente. Você pode fazer isso usando um dos seguintes procedimentos:

* [!DNL flashaccess-i15n.properties] - Amostras incluídas em cada um dos [!DNL .war] arquivos

* [!DNL AdobeInitial.properties] - Amostra localizada na [!DNL /shared] pasta no DVD

   Você pode usar esse arquivo para substituir as propriedades definidas no arquivo WAR da seguinte maneira:

   1. Definir a substituição dos valores de propriedade no [!DNL AdobeInitial.properties]
   1. Local [!DNL AdobeInitial.properties] no classpath.

   >[!NOTE]
   >
   >A Adobe recomenda que você use o [!DNL AdobeInitial.properties] arquivo, já que isso permite que você atualize seus arquivos WAR do aplicativo sem correr o risco de perder qualquer configuração de propriedade anterior que você tenha feito no [!DNL flashaccess-i15n.properties] arquivo.

* O mecanismo de propriedade do Sistema Java.

Você pode aplicar propriedades individuais a esses ambientes de servidor específicos:

* *Desenvolvimento*
* *Estágios*
* *Produção*

Com esse recurso, você pode usar o mesmo arquivo WAR para todos os ambientes de servidor. Para aplicar propriedades a ambientes específicos, anexe dois caracteres de sublinhado (&#39; `__`&#39;) mais um dos seguintes códigos de ambiente para a propriedade *name*:

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Por exemplo, para definir o nível de log como `INFO` para seus servidores de produção e de preparo, e para `DEBUG` para o servidor de desenvolvimento:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

O servidor emprega essa ordem de pesquisa para propriedades:

1. `propertyname_environment` in [!DNL AdobeInitial.properties]

1. `propertyname_environment` in [!DNL flashaccess-15n.properties]

1. `propertyname_environment` nas propriedades do Java System
1. `propertyname` in [!DNL AdobeInitial.properties]

1. `propertyname` in [!DNL flashaccess-15n.properties]

1. `propertyname` nas propriedades do Java System

>[!NOTE]
>
>Você deve especificar o nome do ambiente do servidor como uma propriedade do Java System ao iniciar o servidor. Por exemplo, ao iniciar o Tomcat com [!DNL catalina.bat], defina o `CATALINA_OPTS` variável de ambiente da seguinte maneira:
>-DENVIRONMENT_NAME=[ DEV | ETAPA | PRODUÇÃO ]
