---
description: 'Você deve configurar as propriedades do servidor para refletir seu ambiente. Você pode fazer isso usando qualquer um dos seguintes '
title: Aplicar propriedades a ambientes de servidor
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Aplicar propriedades a ambientes de servidor{#apply-properties-to-server-environments}

Você deve configurar as propriedades do servidor para refletir seu ambiente. Você pode fazer isso usando qualquer um dos seguintes procedimentos:

* [!DNL flashaccess-i15n.properties] - Amostras incluídas em cada uma das [!DNL .war] arquivos

* [!DNL AdobeInitial.properties] - Amostra localizada no [!DNL /shared] no DVD

   Você pode usar esse arquivo para substituir as propriedades definidas no arquivo WAR da seguinte maneira:

   1. Defina os valores da propriedade de substituição em [!DNL AdobeInitial.properties]
   1. Local [!DNL AdobeInitial.properties] no classpath.

   >[!NOTE]
   >
   >O Adobe recomenda que você use o [!DNL AdobeInitial.properties] , já que isso permite atualizar os arquivos WAR do aplicativo sem arriscar a perda de qualquer configuração de propriedade anterior que você tenha feito na [!DNL flashaccess-i15n.properties] arquivo.

* O mecanismo de propriedade Java System.

Você pode aplicar propriedades individuais a esses ambientes de servidor específicos:

* *Desenvolvimento*
* *Estágios*
* *Produção*

Com esse recurso, você pode usar o mesmo arquivo WAR para todos os ambientes de servidor. Para aplicar propriedades a ambientes específicos, anexe dois caracteres sublinhados (&#39; `__`&#39;) mais um dos seguintes códigos de ambiente para a propriedade *name*:

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Por exemplo, para definir o nível de log como `INFO` para seus servidores de produção e de armazenamento temporário e para `DEBUG` para o seu servidor de desenvolvimento:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

O servidor emprega esta ordem de pesquisa para propriedades:

1. `propertyname_environment` em [!DNL AdobeInitial.properties]

1. `propertyname_environment` em [!DNL flashaccess-15n.properties]

1. `propertyname_environment` nas propriedades do Java System
1. `propertyname` em [!DNL AdobeInitial.properties]

1. `propertyname` em [!DNL flashaccess-15n.properties]

1. `propertyname` nas propriedades do Java System

>[!NOTE]
>
>Você deve especificar o nome do ambiente do servidor como uma propriedade do Java System ao iniciar o servidor. Por exemplo, ao iniciar o Tomcat com [!DNL catalina.bat], defina o `CATALINA_OPTS` variável de ambiente da seguinte maneira:
>-DENVIRONMENT_NAME=[ DEV | FASE | PROD ]
