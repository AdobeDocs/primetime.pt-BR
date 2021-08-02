---
title: Uso da linha de comando
description: Uso da linha de comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

* `signaturefile` especifica o caminho para o arquivo signature.xml do aplicativo AIR, localizado no  [!DNL META-INF] diretório de aplicativos

* `signingcert` especifica o certificado usado para assinar o aplicativo AIR

>[!NOTE]
>
>Para determinar a ID do editor de um aplicativo iOS, use a opção `-s` e especifique o certificado usado para assinar o aplicativo iOS. ***A Adobe Primetime é necessária para criar aplicativos iOS que possam reproduzir conteúdo*** protegido por acesso.

