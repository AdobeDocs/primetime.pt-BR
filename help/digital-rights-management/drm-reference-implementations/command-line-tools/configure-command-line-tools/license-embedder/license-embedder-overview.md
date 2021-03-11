---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Embedor da licença DRM {#license-embedder}

Use [!DNL AdobeLicenseEmbedder.jar] para incorporar licenças pré-geradas no conteúdo que o Media Packager protege.

## Uso da linha de comando do Embeder da licença {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` representa um arquivo criptografado.
* `destfile` especifica o nome do arquivo no qual o conteúdo criptografado com a licença incorporada é salvo.

   Se você especificar um diretório, o arquivo será salvo no diretório de destino. O nome do arquivo de origem também se torna o nome do arquivo salvo no diretório de destino.

A tabela a seguir descreve as opções de linha de comando que podem ser especificadas:

**Quadro 7: Opções**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção de linha de comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename  </span> </td> 
   <td colname="2" class="- topic/entry "> Nome do arquivo que inclui a licença que você deseja incorporar. Você pode especificar várias opções <span class="codeph"> -l </span> para incorporar várias licenças. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m nome do arquivo de metadados  </span> </td> 
   <td colname="2" class="- topic/entry "> Especifica os metadados de conteúdo para os quais você pode gerar uma licença. Essa opção é necessária para gerar uma licença. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e o <span class="codeph"> -o </span> não tiver sido aplicado, ocorrerá um erro. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, é possível substituí-lo sem ser solicitado. </td> 
  </tr> 
 </tbody> 
</table>
