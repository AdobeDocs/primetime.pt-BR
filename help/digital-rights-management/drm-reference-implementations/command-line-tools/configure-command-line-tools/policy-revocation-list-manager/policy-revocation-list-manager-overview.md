---
title: Gerenciador de Lista de Revogação DRM
description: Gerenciador de Lista de Revogação DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Gerenciador de Lista de Revogação DRM {#policy-revocation-list-manager}

Usar a ferramenta de linha de comando Gerenciador de Listas de Revogação DRM do Primetime ( [!DNL AdobeRevocationListManager.jar]) para criar e gerenciar listas de revogação e verificar se as políticas foram revogadas.

Antes de executar [!DNL AdobeRevocationListManager.jar], você deve definir as propriedades no *Propriedades do Gerenciador de Listas de Atualização de Políticas e do Gerenciador de Listas de Revogação* seção do seu arquivo de configuração.

>[!NOTE]
>
>Você também pode especificar todas as propriedades do Gerenciador de Listas de Revogação a partir da linha de comando.

## Uso da linha de comando do Gerenciador de Listas de Revogação {#revocation-list-manager-command-line-usage}

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

* `destfile` especifica o nome do arquivo em que as propriedades da lista de revogação são salvas.
* `crlNumber` representa um número de versão não negativo da Lista de Certificados Revogados (CRL). Você precisa incrementar este número sempre que a CRL for atualizada.

**Tabela 5: Opções da linha de comando**

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
   <td colname="2" class="- topic/entry "><p class="- topic/p ">Especifica o nome e o local do arquivo de configuração. </p><p class="- topic/p ">Se você não especificar um nome ou um local, o Gerenciador de Listas de Revogação do DRM procurará <span class="filepath"> flashaccesstools.properties</span> no diretório de trabalho atual. </p><p>Observação: As opções especificadas na linha de comando têm prioridade sobre as opções especificadas no arquivo de configuração. </p>Especifica o local do arquivo de configuração. Se você não aplicar esta opção, o Gerenciador de Listas de Revogação procurará <span class="filepath"> flashaccesstools.properties</span> no diretório de trabalho. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nome do arquivo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Exibe informações sobre a lista de revogação. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e data</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) A data de expiração da lista de revogação. Use um dos seguintes formatos: 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> </li> 
     </ul>Por exemplo, 2009-01-31-14:30:00 representa 31 de janeiro às 14h30. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f arquivo[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Adiciona todas as entradas da lista de revogação existente. Você só pode especificar um arquivo existente. </p> <p class="- topic/p ">Se a lista existente tiver sido assinada com uma credencial diferente daquela usada para assinar a nova lista, será necessário especificar o arquivo de certificado ao lado de verificar a assinatura. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o</span> não estiver definido, ocorrerá um erro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, você poderá substituí-lo sem ser avisado. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r nomeDoEmissorNúmeroSérieDataRevogação</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoga o certificado identificado por <span class="codeph"> IssuerName</span> e <span class="codeph"> serialNumber</span> na data especificada. A variável <span class="codeph"> IssuerName</span> deve usar o formato de nome 509. Por exemplo, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>. </p> <p>Especifique os números de série em um formato hexadecimal. Você também precisa especificar a data de revogação em um dos seguintes formatos: 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> </li> 
     </ul>Por exemplo, 2008-12-1 ou 2008-12-1-00:00:00 para meia-noite de 1º de dezembro de 2008. Se você não especificar a data de revogação, a data atual será aplicada automaticamente. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propriedades de configuração {#configuration-properties}

Você precisa aplicar credenciais para assinar listas de revogação. As seguintes propriedades do Gerenciador de Listas de Revogação especificam um arquivo PKCS12 que inclui credenciais para assinar listas de revogação (Certificado de Servidor de Licença), juntamente com a senha do certificado:

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
