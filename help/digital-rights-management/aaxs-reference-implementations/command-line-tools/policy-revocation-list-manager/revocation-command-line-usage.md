---
seo-title: Uso da linha de comando
title: Uso da linha de comando
uuid: 273e9d3b-efeb-46fa-a4b1-f13247b4e498
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Uso da linha de comando {#command-line-usage}

O Gerenciador de Lista de revogação está no diretório \Reference Implementation\Command Line Tools no DVD. Para executar a ferramenta, use uma das seguintes sintaxes:

```
    java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` indica onde a lista de revogação será escrita.
* `crlNumber` é um número de versão não negativo da Lista de Revogação de Certificado (CRL). Esse número deve ser aumentado toda vez que a CRL for atualizada.

A tabela a seguir contém descrições das opções de linha de comando mostradas na sintaxe acima:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opção de linha de comando </th> 
   <th colname="2" class="- topic/entry entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c configfile</span> </td> 
   <td colname="2" class="- topic/entry ">Especifica o local do arquivo de configuração. Se essa opção não for usada, o Gerenciador de Lista de Revogação procurará <span class="filepath"> flashaccess stools.properties</span> no diretório de trabalho. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nome do arquivo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Exibe informações sobre a lista de revogação. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">Data -e</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) A data de expiração da lista de revogação. Use o formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> ou <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:sec</span> (por exemplo, 2009-01-31-14:30:00 representa 31 de janeiro às 14:30). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">Adiciona todas as entradas da lista de revogação existente. Somente um arquivo existente pode ser especificado. <p class="- topic/p ">Se essa lista existente tiver sido assinada com uma credencial diferente daquela usada para assinar a nova lista, especifique o arquivo de certificado em seguida, para que sua assinatura possa ser verificada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e -o não estiver definido, um erro será retornado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, substitua-o sem solicitar. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r nome do emissor serialNúmeroRevogaçãoData</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoga o certificado identificado por <span class="codeph"> issuersName</span> e <span class="codeph"> serialNumber</span> na data especificada. O <span class="codeph"> emitenteName</span> deve seguir o formato de nome 509 (por exemplo, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). Especifique números de série em forma hexadecimal. Especifique a data de revogação como <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> ou <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:sec</span>, por exemplo 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1 de dezembro, 0008. Se a data de revogação não for especificada, a data atual será usada. </p> </td> 
  </tr> 
 </tbody> 
</table>

