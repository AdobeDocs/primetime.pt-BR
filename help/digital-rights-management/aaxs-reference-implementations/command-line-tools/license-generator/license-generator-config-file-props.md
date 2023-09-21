---
title: Propriedades do arquivo de configuração
description: Propriedades do arquivo de configuração
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Propriedades do arquivo de configuração {#configuration-file-properties}

Antes de executar o License Generator, especifique valores para as propriedades do License Generator. O arquivo de configuração especifica as seguintes propriedades. Para nomes de propriedades que incluem *n*, *n* representa um número inteiro que começa com 1 e aumenta para cada instância da propriedade.

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
   <td colname="2" class="- topic/entry "> Defina a versão mínima do cliente com suporte. Se não estiver definido, por padrão, todas as versões são compatíveis. Defina esse valor para controlar como os clientes mais antigos respondem aos requisitos de licença que não são compatíveis. Especifique x (para o Adobe Access x.0), onde x é o número da versão principal. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificado de servidor de chaves (um certificado de servidor de licenças emitido por Adobe usado pelo servidor de chaves). Esse certificado é usado somente se os metadados/políticas indicarem que um Servidor de chaves é necessário para a entrega de chaves a dispositivos iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> O arquivo PKCS12 que contém as credenciais do License Server para assinatura de licenças. Essa propriedade deve se referir a um arquivo .pfx contendo um certificado e uma chave privada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">A senha usada para proteger o arquivo especificado por <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> Se você estiver gerando licenças de domínio associado, um ou mais certificados de Autoridade de Certificação de Domínio devem ser especificados para indicar as autoridades de domínio confiáveis por esse emissor de licenças. Se o destinatário da licença for um certificado de domínio, que não foi emitido por uma das autoridades de certificação de domínio especificadas, uma licença não poderá ser gerada. Essa propriedade especifica um arquivo .cer que contém somente o certificado (o formato PEM ou DER é aceitável). n deve aumentar monotonicamente, começando em 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Arquivo PKCS12 opcional contendo credenciais adicionais do License Server para descriptografar o CEK nos metadados e na política. Credenciais adicionais podem ser configuradas se o conteúdo tiver sido previamente empacotado com um certificado de Servidor de Licenças diferente do especificado por <span class="codeph"> licensegen.sign.certfile</span>. Essa propriedade deve se referir a um <span class="filepath"> .pfx</span> arquivo que contém um certificado e uma chave privada. n deve aumentar monotonicamente, começando em 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">A senha usada para proteger o arquivo especificado por: <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>
