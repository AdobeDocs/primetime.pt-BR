---
title: Uso da linha de comando
description: Uso da linha de comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
* `destfile` especifica onde o conteúdo criptografado com a licença incorporada será gravado. Se um diretório for especificado, o arquivo será salvo nesse diretório usando o mesmo nome do arquivo de origem, mas o diretório não deve ser o diretório que contém o arquivo de origem.

A tabela a seguir descreve as opções de linha de comando que podem ser especificadas com a sintaxe mencionada anteriormente:

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
   <td colname="2" class="- topic/entry "> Nome do arquivo que contém a licença a ser incorporada. Múltiplo <span class="codeph"> -l </span> opções podem ser especificadas para incorporar várias licenças. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m nome do arquivo de metadados </span> </td> 
   <td colname="2" class="- topic/entry "> Especifique os metadados de conteúdo para os quais gerar uma licença. (Obrigatório para gerar a licença) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o </span> não estiver definido, um erro será retornado. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, substitua-o sem avisar. </td> 
  </tr> 
 </tbody> 
</table>
