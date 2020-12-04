---
seo-title: Uso da linha de comando
title: Uso da linha de comando
uuid: 72117619-a723-49d3-9aa9-5eefcf5b0916
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Uso da linha de comando {#command-line-usage}

Para incorporar uma licença, use a seguinte sintaxe:

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` é um arquivo FLV ou F4V criptografado.
* `destfile` especifica onde o conteúdo criptografado com a licença incorporada será gravado. Se um diretório for especificado, o arquivo será salvo nesse diretório usando o mesmo nome de arquivo que o arquivo de origem, mas o diretório não deve ser o diretório que contém o arquivo de origem.

A tabela a seguir descreve as opções de linha de comando que podem ser especificadas junto com a sintaxe mencionada anteriormente:

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
   <td colname="2" class="- topic/entry "> Nome do arquivo que contém a licença a ser incorporada. Várias opções <span class="codeph"> -l </span> podem ser especificadas para incorporar várias licenças. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename  </span> </td> 
   <td colname="2" class="- topic/entry "> Especifique os metadados de conteúdo para os quais gerar uma licença. (Obrigatório para gerar licença) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o </span> não estiver definido, um erro será retornado. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, substitua-o sem solicitar. </td> 
  </tr> 
 </tbody> 
</table>

