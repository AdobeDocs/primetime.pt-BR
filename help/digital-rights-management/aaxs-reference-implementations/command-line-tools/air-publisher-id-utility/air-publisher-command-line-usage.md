---
title: Uso da linha de comando
description: Uso da linha de comando
copied-description: true
exl-id: 67056085-beb5-4f54-8962-369bc32d7907
source-git-commit: 79cab347d0daa01549fbf8a9b37bf0a91c14648e
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Uso da linha de comando {#command-line-usage}

Para executar a ferramenta, use a seguinte sintaxe:

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

* `signaturefile` especifica o caminho para o arquivo signature.xml do aplicativo AIR, localizado nos aplicativos [!DNL META-INF] diretory

* `signingcert` especifica o certificado usado para assinar o aplicativo AIR

>[!NOTE]
>
>Para determinar a ID do publicador de um aplicativo do iOS, use a variável `-s` e especifique o certificado usado para assinar o aplicativo do iOS. ***O Adobe Primetime é necessário para criar aplicativos iOS que possam reproduzir conteúdo protegido pelo acesso***.
