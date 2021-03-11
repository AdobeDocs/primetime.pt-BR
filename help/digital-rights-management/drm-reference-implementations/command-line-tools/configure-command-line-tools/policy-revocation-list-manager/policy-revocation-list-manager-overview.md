---
title: Gerenciador da lista de revogação de DRM
description: Gerenciador da lista de revogação de DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Gerenciador de lista de revogação de DRM {#policy-revocation-list-manager}

Use a ferramenta de linha de comando do Gerenciador de Lista de Revogação de DRM do Primetime ( [!DNL AdobeRevocationListManager.jar]) para criar e gerenciar listas de revogação e verificar se as políticas foram revogadas.

Antes de executar [!DNL AdobeRevocationListManager.jar], você deve definir as propriedades na seção *Gerenciador de lista de atualização de política e Propriedades do gerenciador de lista de revogação* do arquivo de configuração.

>[!NOTE]
>
>Também é possível especificar todas as propriedades do Gerenciador de lista de revogação na linha de comando.

## Uso da linha de comando do Gerenciador de Lista de Revogação {#revocation-list-manager-command-line-usage}

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

* `destfile` especifica o nome do arquivo no qual as propriedades da lista de revogação são salvas.
* `crlNumber` representa um número de versão não negativo da Lista de Revogação de Certificados (CRL). Você precisa incrementar esse número sempre que a CRL for atualizada.

**Quadro 5: Opções de linha de comando**

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
   <td colname="2" class="- topic/entry "><p class="- topic/p ">Especifica o nome e o local do arquivo de configuração. </p><p class="- topic/p ">Se você não especificar um nome ou um local, o Gerenciador de Lista de Revogação de DRM procura <span class="filepath"> flashaccess.properties</span> no diretório de trabalho atual. </p><p>Observação:  As opções especificadas na linha de comando têm prioridade sobre as opções especificadas no arquivo de configuração. </p>Especifica o local do arquivo de configuração. Se você não aplicar essa opção, o Gerenciador de Lista de Revogação procurará <span class="filepath"> flashaccess stools.properties</span> no diretório de trabalho. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nome do arquivo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Exibe informações sobre a lista de revogação. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">data -e</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) A data de expiração da lista de revogação. Use um dos seguintes formatos: 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:seg</span> </li> 
     </ul>Por exemplo, 2009-01-31-14:30:00 representa 31 de janeiro às 2:30 PM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Adiciona todas as entradas da lista de revogação existente. Você só pode especificar um arquivo existente. </p> <p class="- topic/p ">Se a lista existente foi assinada com uma credencial diferente da usada para assinar a nova lista, é necessário especificar o arquivo de certificado ao lado para verificar a assinatura. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o</span> não estiver definido, ocorrerá um erro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, é possível substituí-lo sem ser solicitado. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r nome do emissor serialNúmeroRevogaçãoData</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoga o certificado que foi identificado por <span class="codeph"> emitenteName</span> e <span class="codeph"> serialNumber</span> na data especificada. O <span class="codeph"> emitenteName</span> deve usar o formato de nome 509. Por exemplo, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>. </p> <p>Você deve especificar os números de série em um formato hexadecimal. Também é necessário especificar a data de revogação em um dos seguintes formatos: 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:seg</span> </li> 
     </ul>Por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1º de dezembro de 2008. Se você não especificar a data de revogação, a data atual será aplicada automaticamente. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propriedades de configuração {#configuration-properties}

Você precisa aplicar credenciais para assinar listas de revogação. As seguintes propriedades do Gerenciador de Lista de Revogação especificam um arquivo PKCS12 que inclui credenciais para a assinatura de listas de revogação (Certificado do Servidor de Licenças), juntamente com a senha do certificado:

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`