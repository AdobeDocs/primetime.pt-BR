---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Utilitário de ID do editor do AIR {#air-publisher-id-utility}

Quando você cria um arquivo do AIR, a Ferramenta de desenvolvedor do AIR (ADT) gera automaticamente uma ID do editor. O utilitário AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcula a Publisher ID para um aplicativo AIR.

A Publisher ID é exclusiva do certificado usado para criar um arquivo AIR. Se você reutilizar o mesmo certificado para vários aplicativos AIR, todos os aplicativos AIR terão a mesma Publisher ID. Uma versão do AIR que tenha êxito na versão 1.5.2 não adiciona a ID do editor gerada a um arquivo. Portanto, se você planeja usar uma lista de permissões de aplicativo do AIR, use essa ferramenta para determinar a Publisher ID.

>[!NOTE]
>
>A ID do Editor usada para a imposição da lista de permissões do AIR não é a mesma ID do Editor que o publicador do aplicativo especifica no arquivo [!DNL application.xml] do aplicativo.

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

* 
   * `signaturefile`* especifica um caminho para o  [!DNL signatures.xml] arquivo do aplicativo AIR, localizado no  [!DNL META-INF] diretório de aplicativos

* `signingcert` especifica o certificado usado para assinar um aplicativo AIR

>[!NOTE]
>
>Para determinar a ID do publicador de um aplicativo Android, é necessário usar a opção `-s` para especificar o certificado usado para assinar o pacote de aplicativo Android (APK). O DRM do Primetime é necessário para criar aplicativos Android que possam reproduzir conteúdo protegido por DRM do Primetime.