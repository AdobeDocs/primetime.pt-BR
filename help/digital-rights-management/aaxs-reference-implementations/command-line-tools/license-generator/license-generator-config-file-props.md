---
title: Propriedades do arquivo de configuração
description: Propriedades do arquivo de configuração
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Propriedades do arquivo de configuração {#configuration-file-properties}

Antes de executar o Gerador de Licenças, especifique os valores para as propriedades do Gerador de Licenças. O arquivo de configuração especifica as seguintes propriedades. Para nomes de propriedades que incluem *n*, *n* representa um número inteiro que começa com 1 e aumenta para cada instância da propriedade.

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
   <td colname="2" class="- topic/entry "> Defina a versão mínima do cliente suportada. Se não estiver definido, por padrão, todas as versões serão compatíveis. Defina esse valor para controlar como os clientes mais antigos respondem aos requisitos de licença que não suportam. Especifique x (para Acesso ao Adobe x.0), onde x é o número da versão principal. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificado do Servidor de Chave (um certificado do Servidor de Licenças emitido pelo Adobe usado pelo Servidor de Chave). Esse certificado é usado somente se os metadados/política indicarem que um Servidor de chaves é necessário para entrega de chaves a dispositivos iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> O arquivo PKCS12 contendo as credenciais do License Server para assinatura de licenças. Essa propriedade deve se referir a um arquivo .pfx contendo um certificado e uma chave privada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">A senha usada para proteger o arquivo especificado por <span class="+ topic/ph pr-d/codeph codeph"> license.sign.certfile.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> Se estiver gerando licenças vinculadas ao domínio, um ou mais certificados de autoridade de certificação de domínio devem ser especificados para indicar as autoridades de domínio confiáveis por esse emissor de licença. Se o recipient da licença for um certificado de domínio, que não foi emitido por uma das CAs de domínio especificadas, uma licença não poderá ser gerada. Essa propriedade especifica um arquivo .cer que contém somente o certificado (o formato PEM ou DER é aceitável). n deve aumentar monotonicamente, a partir de 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Arquivo PKCS12 opcional contendo credenciais adicionais do License Server para descriptografar o CEK nos metadados e na política. Credenciais adicionais podem ser configuradas se o conteúdo tiver sido empacotado anteriormente com um certificado do License Server diferente do especificado por <span class="codeph"> license.sign.certfile</span>. Essa propriedade deve se referir a um arquivo <span class="filepath"> .pfx</span> contendo um certificado e uma chave privada. n deve aumentar monotonicamente, a partir de 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">A senha usada para proteger o arquivo especificado por: <p><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

