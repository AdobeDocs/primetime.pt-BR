---
seo-title: Uso da linha de comando
title: Uso da linha de comando
uuid: 54b1e867-c6cc-4355-b8e6-a7ec910bd33d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

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

* 
   * `signaturefile`* especifica o caminho para o arquivo signature.xml do aplicativo AIR, localizado no [!DNL META-INF] diretório de aplicativos

* `signingcert` especifica o certificado usado para assinar o aplicativo AIR

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Para determinar a ID do editor para um aplicativo iOS, use a `-s` opção e especifique o certificado usado para assinar o aplicativo iOS. ***O Adobe Primetime é necessário para criar aplicativos iOS que podem reproduzir conteúdo*** protegido por acesso.

