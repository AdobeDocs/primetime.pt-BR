---
title: Visão geral
description: Visão geral
copied-description: true
exl-id: 07f2ef0b-c6aa-4574-a3ae-18685a090cf2
source-git-commit: a1fc67b708f3d5821532d3827639adbadf15f6b4
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Utilitário AIR Publisher ID {#air-publisher-id-utility}

Quando você cria um arquivo AIR, a Ferramenta de desenvolvedor do AIR (ADT) gera automaticamente uma ID do editor. O utilitário AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcula a Publisher ID para um aplicativo do AIR.

A Publisher ID é exclusiva ao certificado usado para criar um arquivo AIR. Se você reutilizar o mesmo certificado para vários aplicativos AIR, todos os aplicativos AIR terão a mesma Publisher ID. Uma versão do AIR que tenha êxito na versão 1.5.2 não adiciona a Publisher ID gerada a um arquivo. Portanto, se você planeja usar uma lista de permissões de aplicativo do AIR, use essa ferramenta para determinar a Publisher ID.

>[!NOTE]
>
>A ID do editor usada para a imposição da lista de permissões do AIR não é a mesma ID do editor que o editor do aplicativo especifica no [!DNL application.xml] arquivo.

## Uso da linha de comando do utilitário AIR Publisher ID {#air-publisher-id-utility-command-line-usage}

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `signaturefile` especifica um caminho para o aplicativo do AIR [!DNL signatures.xml] , localizado nos aplicativos [!DNL META-INF] diretory

* `signingcert` especifica o certificado usado para assinar um aplicativo AIR

>[!NOTE]
>
>Para determinar a ID do publicador de um aplicativo Android, é necessário usar a variável `-s` para especificar o certificado usado para assinar o pacote de aplicativo Android (APK). O DRM do Primetime é necessário para criar aplicativos Android que possam reproduzir conteúdo protegido por DRM do Primetime.
