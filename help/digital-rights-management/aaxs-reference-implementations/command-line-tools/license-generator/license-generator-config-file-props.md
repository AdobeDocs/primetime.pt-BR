---
seo-title: Propriedades do arquivo de configuração
title: Propriedades do arquivo de configuração
uuid: 13e158a6-c447-4e5e-884d-03fb4835c120
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
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
   <td colname="2" class="- topic/entry "> Defina a versão mínima do cliente suportada. Se não estiver definido, por padrão, todas as versões são suportadas. Defina esse valor para controlar como os clientes mais antigos respondem aos requisitos de licença que não suportam. Especifique x (para Adobe Access x.0), onde x é o número principal da versão. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificado do Servidor de Chaves (um certificado do Servidor de Licenças emitido por Adobe usado pelo Servidor de Chaves). Este certificado é usado somente se os metadados/política indicarem que um Servidor de chaves é necessário para o delivery de chaves para dispositivos iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> O arquivo PKCS12 que contém as credenciais do License Server para assinatura de licenças. Essa propriedade deve se referir a um arquivo .pfx contendo um certificado e uma chave privada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">A senha usada para proteger o arquivo especificado por <span class="+ topic/ph pr-d/codeph codeph"> licenseSegen.sign.certfile.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> Se você estiver gerando licenças vinculadas a domínio, um ou mais certificados de CA de domínio devem ser especificados para indicar as autoridades de domínio confiáveis por esse emissor de licença. Se o recipient de licença for um certificado de domínio, que não foi emitido por uma das CAs de domínio especificadas, não será possível gerar uma licença. Essa propriedade especifica um arquivo .cer que contém somente o certificado (o formato PEM ou DER é aceitável). n deve estar aumentando monotonicamente, a partir de 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Arquivo PKCS12 opcional contendo credenciais adicionais do License Server para descriptografar o CEK nos metadados e na política. Poderão ser configuradas credenciais adicionais se o conteúdo tiver sido previamente empacotado com um certificado do License Server diferente daquele especificado por <span class="codeph"> licencisegen.sign.certfile</span>. Essa propriedade deve se referir a um arquivo <span class="filepath"> .pfx</span> que contém um certificado e uma chave privada. n deve estar aumentando monotonicamente, a partir de 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">A senha usada para proteger o arquivo especificado por: <p><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

