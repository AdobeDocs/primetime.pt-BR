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

# Utilitário de ID do AIR Publisher {#air-publisher-id-utility}

Ao criar um arquivo do AIR, a Ferramenta de desenvolvedor do AIR (ADT) gera automaticamente uma ID do editor. O utilitário AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcula a ID do editor de um aplicativo do AIR.

A ID do editor é exclusiva ao certificado usado para criar um arquivo do AIR. Se você reutilizar o mesmo certificado para vários aplicativos do AIR, todos os aplicativos do AIR terão a mesma ID do editor. Uma versão do AIR que sucede a versão 1.5.2 não adiciona a ID do editor gerada a um arquivo. Portanto, se você planeja usar uma lista de permissões de aplicativo do AIR, use essa ferramenta para determinar a ID do editor.

>[!NOTE]
>
>A ID do Publicador usada para imposição de lista de permissões do AIR não é a mesma que a ID do Publicador especificada pelo editor do aplicativo [!DNL application.xml] arquivo.

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

* `signaturefile` especifica um caminho para o aplicativo AIR [!DNL signatures.xml] arquivo, localizado nos aplicativos [!DNL META-INF] diretório

* `signingcert` especifica o certificado usado para assinar um aplicativo do AIR

>[!NOTE]
>
>Para determinar a ID do editor de um aplicativo Android, é necessário usar o `-s` opção para especificar o certificado usado para assinar o pacote de aplicativo do Android (APK). O DRM do Primetime é necessário para criar aplicativos Android que possam reproduzir conteúdo protegido por DRM do Primetime.
