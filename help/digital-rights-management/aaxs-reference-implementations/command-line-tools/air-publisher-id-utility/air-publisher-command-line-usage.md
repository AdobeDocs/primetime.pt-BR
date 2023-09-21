---
title: Uso da linha de comando
description: Uso da linha de comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

* `signaturefile` especifica o caminho para o arquivo signatures.xml do aplicativo AIR, localizado nos aplicativos [!DNL META-INF] diretório

* `signingcert` especifica o certificado usado para assinar o aplicativo AIR

>[!NOTE]
>
>Para determinar a ID do editor de um aplicativo do iOS, use o `-s` e especifique o certificado usado para assinar o aplicativo do iOS. ***O Adobe Primetime é necessário para criar aplicativos iOS que possam reproduzir conteúdo protegido de acesso***.
