---
seo-title: Visão geral
title: Visão geral
uuid: 5487d1d3-7eb8-410d-a4b1-cde3e94c00a1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Embeder de licença DRM {#license-embedder}

Use [!DNL AdobeLicenseEmbedder.jar] para incorporar licenças pré-geradas ao conteúdo protegido pelo Media Packager.

## Uso da linha de comando do Embeder de licença {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` representa um arquivo criptografado.
* `destfile` especifica o nome do arquivo no qual o conteúdo criptografado com a licença incorporada é salvo.

   Se você especificar um diretório, o arquivo será salvo no diretório de destino. O nome do arquivo de origem também se torna o nome do arquivo salvo no diretório de destino.

A tabela a seguir descreve as opções de linha de comando que você pode especificar:

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
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l nome do arquivo  </span> </td> 
   <td colname="2" class="- topic/entry "> Nome do arquivo que inclui a licença que você deseja incorporar. Você pode especificar várias opções <span class="codeph"> -l </span> para incorporar várias licenças. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename  </span> </td> 
   <td colname="2" class="- topic/entry "> Especifica os metadados de conteúdo para os quais você pode gerar uma licença. Essa opção é necessária para gerar uma licença. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o </span> não tiver sido aplicado, ocorrerá um erro. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, você poderá substituí-lo sem ser solicitado. </td> 
  </tr> 
 </tbody> 
</table>
