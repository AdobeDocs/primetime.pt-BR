---
title: Visão geral
description: Visão geral
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Incorporador da licença de DRM {#license-embedder}

Uso [!DNL AdobeLicenseEmbedder.jar] para incorporar licenças pré-geradas em conteúdo protegido pelo Media Packager.

## Uso da linha de comando do License Embedder {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` representa um arquivo criptografado.
* `destfile` especifica o nome do arquivo no qual o conteúdo criptografado com a licença incorporada é salvo.

  Se você especificar um diretório, o arquivo será salvo no diretório de destino. O nome do arquivo de origem também se torna o nome do arquivo salvo no diretório de destino.

A tabela a seguir descreve as opções de linha de comando que você pode especificar:

**Tabela 7: Opções**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção de linha de comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l licença-arquivo </span> </td> 
   <td colname="2" class="- topic/entry "> Nome do arquivo que inclui a licença que você deseja incorporar. É possível especificar vários <span class="codeph"> -l </span> opções para incorporar várias licenças. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m nome do arquivo de metadados </span> </td> 
   <td colname="2" class="- topic/entry "> Especifica os metadados de conteúdo para os quais você pode gerar uma licença. Esta opção é necessária para gerar uma licença. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e a variável <span class="codeph"> -o </span> não foi aplicado, ocorre um erro. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, você poderá substituí-lo sem ser avisado. </td> 
  </tr> 
 </tbody> 
</table>
