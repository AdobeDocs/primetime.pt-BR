---
seo-title: Visão geral
title: Visão geral
uuid: 857390be-dd14-46c0-b8f7-2bc661c515d4
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# Gerador de licença DRM {#license-generator}

Use [!DNL AdobeLicenseGenerator.jar] para gerar licenças sem exigir que o cliente envie uma solicitação de licença a um servidor. Em seguida, você pode incorporar uma licença pré-gerada no conteúdo ou fornecer a licença ao cliente por meio de outros mecanismos, como um servidor Web HTTP simples.

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

* `metadata` - Inclui os metadados do Adobe Primetime DRM.

   Você pode recuperar esse arquivo do conteúdo protegido com as opções `-d -m` no Media Packager.

**Exibir uma licença gerada anteriormente:**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` - Contém uma licença Adobe Primetime DRM gerada pelo Gerador de licenças.

**Quadro 6: Opções**

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nome e o local do arquivo de configuração. </p> <p class="- topic/p ">Se você não especificar um nome ou um local, o DRM License Generator procurará <span class="filepath"> flashaccess stools.properties</span> no diretório de trabalho atual. </p> <p>Observação:  As opções especificadas na linha de comando têm prioridade sobre as opções especificadas no arquivo de configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> arquivo licenciado</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Exibe informações sobre uma licença que já foi gerada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-folha de nome de arquivo</span> </td> 
   <td colname="2" class="- topic/entry "> Gera uma licença de folha e salva a saída em um arquivo especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Especifica os metadados de conteúdo para os quais você precisa gerar uma licença. Essa opção é necessária para gerar uma licença. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o</span> não tiver sido definido, ocorrerá um erro. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, você poderá substituí-lo sem ser solicitado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se os metadados incluírem várias políticas de DRM, é possível especificar o número de políticas de DRM que podem ser usadas para gerar uma licença. </p> <p>Se você não especificar o número de políticas de DRM, a primeira política de DRM será aplicada automaticamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r certificado de recipient</span> </td> 
   <td colname="2" class="- topic/entry ">Gera uma licença para um recipient especificado. Você pode usar um dispositivo ou certificado de domínio e pode especificar várias <span class="+ topic/ph pr-d/codeph codeph"> -r </span>opções para criar uma licença para vários recipient. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Gera uma licença raiz e salva a saída em um arquivo que você especificar. </td> 
  </tr> 
 </tbody> 
</table>

## Propriedades do arquivo de configuração {#configuration-file-properties}

Antes de executar o License Generator, é necessário especificar valores para as propriedades do License Generator no arquivo de configuração.

>[!NOTE]
>
>Para nomes de propriedades que incluem *n*, *n* representa um número inteiro que start com 1 e aumenta para cada instância da propriedade.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Propriedade </th> 
   <th colname="2" class="- topic/entry entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Define a versão mínima do cliente atualmente compatível. Se você não definir essa propriedade, todas as versões serão automaticamente suportadas por padrão. </p> <p>Você pode definir esse valor para controlar como os clientes mais antigos respondem aos requisitos de licença que eles não suportam. Especifique <span class="codeph"> x</span> (para Adobe Primetime DRM x.0) onde <span class="codeph"> x</span> representa um número de versão principal. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificado de Servidor de Chaves, que é um certificado de Servidor de Licenças emitido por Adobe, usado pelo Servidor de Chaves. Este certificado é aplicado somente se a política de metadados/DRM indicar que um Servidor de chaves é necessário para o delivery de chaves para dispositivos iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> O arquivo PKCS12 que inclui as credenciais do License Server para a assinatura de licenças. Essa propriedade precisa se referir a um arquivo .pfx que inclui um certificado e uma chave privada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">A senha que protege o arquivo especificado com a opção <span class="+ topic/ph pr-d/codeph codeph"> license.sign.certfile</span>. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Se você gerar licenças vinculadas a domínio, deverá especificar um ou mais certificados de CA de domínio para indicar as autoridades de domínio em que o emissor da licença pode confiar. </p> <p>Se o recipient de licença for um certificado de domínio, que não foi emitido por uma das CAs de domínio especificadas, não será possível gerar uma licença. Esta propriedade especifica um arquivo <span class="filepath"> .cer</span> que inclui o certificado no formato PEM ou DER. <span class="codeph">Não </span> deve aumentar monotonicamente, a partir de 1. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Arquivo PKCS12 opcional que inclui credenciais adicionais do License Server para descriptografar o CEK na política de metadados e DRM. Você pode configurar credenciais adicionais se o conteúdo tiver sido previamente empacotado com um certificado do License Server diferente daquelas credenciais que foram especificadas com <span class="codeph"> licencisegen.sign.certfile</span>. Essa propriedade precisa fazer referência a um arquivo <span class="filepath"> .pfx</span> que inclui um certificado e uma chave privada. <span class="codeph">Não </span> deve aumentar monotonicamente, a partir de 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>A senha é aplicada para proteger o arquivo especificado com a propriedade<span class="+ topic/ph pr-d/codeph codeph"> licenseSegen.keys.asymmetric.licenseServerCredential.n</span>. </p> </td> 
  </tr> 
 </tbody> 
</table>