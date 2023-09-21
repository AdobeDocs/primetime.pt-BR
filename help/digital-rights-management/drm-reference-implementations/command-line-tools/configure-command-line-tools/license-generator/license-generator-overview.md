---
title: Visão geral
description: Visão geral
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Gerador de licença DRM {#license-generator}

Uso [!DNL AdobeLicenseGenerator.jar] para gerar licenças sem exigir que o cliente envie uma solicitação de licença para um servidor. Você pode então incorporar uma licença pré-gerada no conteúdo ou entregar a licença ao cliente por meio de outros mecanismos, como um simples servidor Web HTTP.

## Uso da linha de comando do License Generator {#license-generator-command-line-usage}

**Gerar uma licença:**

```
java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

* `metadata` - Inclui os metadados de DRM do Adobe Primetime.

  Você pode recuperar esse arquivo do conteúdo protegido com o `-d -m` opções no Media Packager.

**Exibir uma licença gerada anteriormente:**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` - Contém uma licença DRM do Adobe Primetime gerada pelo Gerador de Licenças.

**Tabela 6: Opções**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção de linha de comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c configfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nome e o local do arquivo de configuração. </p> <p class="- topic/p ">Se você não especificar um nome ou um local, o Gerador de Licenças DRM procurará <span class="filepath"> flashaccesstools.properties</span> no diretório de trabalho atual. </p> <p>Observação: As opções especificadas na linha de comando têm prioridade sobre as opções especificadas no arquivo de configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> arquivo de licença</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Exibe informações sobre uma licença já gerada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf-leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Gera uma licença folha e salva a saída em um arquivo especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m nome do arquivo de metadados</span> </td> 
   <td colname="2" class="- topic/entry "> Especifica os metadados de conteúdo para os quais você precisa gerar uma licença. Esta opção é necessária para gerar uma licença. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e a variável <span class="codeph"> -o</span> não foi definido, ocorre um erro. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, você poderá substituí-lo sem ser avisado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se os metadados incluírem várias políticas de DRM, você poderá especificar o número de políticas de DRM que podem ser usadas para gerar uma licença. </p> <p>Se você não especificar o número de políticas DRM, a primeira política DRM será aplicada automaticamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">Gera uma licença para um determinado destinatário. Você pode usar um dispositivo ou certificado de domínio e pode especificar vários <span class="+ topic/ph pr-d/codeph codeph"> -r </span>opções para criar uma licença para vários recipients. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root nome-do-arquivo</span> </td> 
   <td colname="2" class="- topic/entry "> Gera uma licença raiz e salva a saída em um arquivo especificado por você. </td> 
  </tr> 
 </tbody> 
</table>

## Propriedades do arquivo de configuração {#configuration-file-properties}

Antes de executar o License Generator, você precisa especificar valores para as propriedades do License Generator no arquivo de configuração.

>[!NOTE]
>
>Para nomes de propriedades que incluem *n*, *n* representa um número inteiro que começa com 1 e aumenta para cada instância da propriedade.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Propriedade </th> 
   <th colname="2" class="- topic/entry entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Define a versão mínima do cliente com suporte no momento. Se você não definir essa propriedade, todas as versões serão automaticamente compatíveis por padrão. </p> <p>Você pode definir esse valor para controlar como os clientes mais antigos respondem aos requisitos de licença que não são compatíveis. Especificar <span class="codeph"> x</span> (para Adobe Primetime DRM x.0) onde <span class="codeph"> x</span> representa um número de versão principal. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificado do servidor de chaves, que é um certificado de servidor de licenças emitido por Adobe usado pelo servidor de chaves. Esse certificado é aplicado somente se a política de metadados/DRM indicar que um Servidor de chaves é necessário para a entrega de chaves a dispositivos iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> O arquivo PKCS12 que inclui as credenciais do License Server para assinatura de licenças. Essa propriedade precisa se referir a um arquivo .pfx que inclua um certificado e uma chave privada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">A senha que protege o arquivo especificado com o <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> opção. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se você gerar licenças vinculadas a domínio, deverá especificar um ou mais certificados da Autoridade de Certificação de Domínio para indicar as autoridades de domínio nas quais o emissor da licença pode confiar. </p> <p>Se o destinatário da licença for um certificado de domínio, que não foi emitido por uma das autoridades de certificação de domínio especificadas, uma licença não poderá ser gerada. Esta propriedade especifica uma <span class="filepath"> .cer</span> arquivo que inclui o certificado no formato PEM ou DER. <span class="codeph">n</span> deve aumentar monotonicamente, a partir de 1. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Arquivo PKCS12 opcional que inclui credenciais adicionais do License Server para descriptografar o CEK na política de metadados e DRM. Você pode configurar credenciais adicionais se o conteúdo tiver sido empacotado com um certificado do License Server diferente daquelas credenciais especificadas com o <span class="codeph"> licensegen.sign.certfile</span>. Esta propriedade precisa se referir a um <span class="filepath"> .pfx</span> arquivo que inclui um certificado e uma chave privada. <span class="codeph">n</span> deve aumentar monotonicamente, a partir de 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>A senha é aplicada para proteger o arquivo especificado com o<span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> propriedade. </p> </td> 
  </tr> 
 </tbody> 
</table>
