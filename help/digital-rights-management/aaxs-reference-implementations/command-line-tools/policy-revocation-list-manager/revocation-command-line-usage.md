---
title: Uso da linha de comando
description: Uso da linha de comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Uso da linha de comando {#command-line-usage}

O Revocation List Manager está no diretório \Reference Implementation\Command Line Tools no DVD. Para executar a ferramenta, use uma das seguintes sintaxes:

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

* `destfile` indica onde a lista de revogação será gravada.
* `crlNumber` é um número de versão não negativo da Lista de Certificados Revogados (CRL). Esse número deve ser incrementado sempre que a CRL for atualizada.

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
   <td colname="2" class="- topic/entry ">Especifica o local do arquivo de configuração. Se essa opção não for usada, o Gerenciador de Listas de Revogação procurará <span class="filepath"> flashaccesstools.properties</span> no diretório de trabalho. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nome do arquivo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Exibe informações sobre a lista de revogação. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e data</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) A data de expiração da lista de revogação. Usar o formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> ou <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> (por exemplo, 31-01-2009):30:00 representa 31 de janeiro às 14h30). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f arquivo[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">Adiciona todas as entradas da lista de revogação existente. Somente um arquivo existente pode ser especificado. <p class="- topic/p ">Se essa lista existente tiver sido assinada com uma credencial diferente da que está sendo usada para assinar a nova lista, especifique o arquivo de certificado em seguida, para que a assinatura possa ser verificada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e -o não estiver definido, um erro será retornado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, substitua-o sem avisar. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r nomeDoEmissorNúmeroSérieDataRevogação</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoga o certificado identificado por <span class="codeph"> IssuerName</span> e <span class="codeph"> serialNumber</span> na data especificada. A variável <span class="codeph"> IssuerName</span> deve seguir o formato de nome 509 (por exemplo, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). Especifique números de série em formato hexadecimal. Especificar a data de revogação como <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> ou <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span>, por exemplo 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1º de dezembro de 2008. Se a data de revogação não for especificada, a data atual será usada. </p> </td> 
  </tr> 
 </tbody> 
</table>
