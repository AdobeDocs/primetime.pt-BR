---
seo-title: Visão geral
title: Visão geral
uuid: f45c6b58-53c5-41e0-be3d-590231dd214a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Utilitário de ID do editor do AIR {#air-publisher-id-utility}

Quando você cria um arquivo AIR, a AIR Developer Tool (ADT) gera automaticamente uma Publisher ID. O utilitário AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcula a Publisher ID para um aplicativo AIR.

A Publisher ID é exclusiva do certificado usado para criar um arquivo AIR. Se você reutilizar o mesmo certificado para vários aplicativos AIR, todos os aplicativos AIR terão a mesma Publisher ID. Uma versão do AIR com êxito na versão 1.5.2 não adiciona a ID do editor gerada a um arquivo. Portanto, se você planeja usar uma lista de permissões de aplicativo AIR, use essa ferramenta para determinar a ID do editor.

>[!NOTE]
>
>A ID do editor usada para a imposição de lista de permissões do AIR não é a mesma ID do editor que o editor do aplicativo especifica no [!DNL application.xml] arquivo do aplicativo.

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
   * `signaturefile`* especifica um caminho para o arquivo do aplicativo AIR, localizado no [!DNL signatures.xml] diretório de aplicativos [!DNL META-INF]

* `signingcert` especifica o certificado usado para assinar um aplicativo AIR

>[!NOTE]
>
>Para determinar a ID do editor para um aplicativo Android, é necessário usar a `-s` opção para especificar o certificado usado para assinar o pacote de aplicativo Android (APK). O Primetime DRM é necessário para criar aplicativos Android que possam reproduzir conteúdo protegido por DRM Primetime.