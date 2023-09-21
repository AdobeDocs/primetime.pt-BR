---
title: Propriedades do arquivo de configuração
description: Propriedades do arquivo de configuração
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Propriedades do arquivo de configuração {#configuration-file-properties}

Antes de executar o Media Packager, especifique valores para as propriedades do Media Packager. O arquivo de configuração especifica as seguintes propriedades. Para nomes de propriedades que incluem* n*, *n* representa um número inteiro que começa com 1 e aumenta para cada instância da propriedade.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Propriedade </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se o conteúdo de vídeo deve ser criptografado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se o áudio deve ser criptografado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se os dados de script devem ser criptografados em FLVs. <i class="+ topic/ph hi-d/i ">onMetaData</i> e <i class="+ topic/ph hi-d/i ">onXMP</i> as tags de dados de script nunca são criptografadas, mesmo se essa opção estiver ativada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica o nível de criptografia do vídeo. Um valor alto é usado para criptografar todo o conteúdo de vídeo, enquanto valores médios e baixos são usados para criptografar partes do conteúdo de vídeo para arquivos F4V que contêm conteúdo H.264. </p> <p class="- topic/p ">value = <span class="codeph"> alta | médio | baixa</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se o valor for maior que 0, o número especificado de segundos de conteúdo no início do arquivo não será criptografado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O arquivo de certificado do servidor de licenças usado para criptografar a chave. A variável <span class="codeph"> encrypt.keys.asymmetric.certfile</span> A propriedade especifica um arquivo que contém somente o certificado (o formato PEM ou DER é aceitável). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Essa propriedade é usada repetidamente para criar uma lista de políticas a serem aplicadas ao conteúdo. <span class="codeph"> n</span> é um número inteiro cujo valor é 1 ou maior. O cliente usará a primeira instância por padrão. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O URL do servidor de licenças. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O certificado de transporte do servidor de licenças. Esta propriedade especifica uma <span class="filepath"> .cer</span> arquivo que contém somente o certificado (o formato PEM ou DER é aceitável). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O arquivo PKCS12 que contém credenciais de empacotador para assinatura de conteúdo. A variável <span class="codeph"> encrypt.sign.certfile</span> deve referir-se a um <span class="filepath"> .pfx</span> arquivo que contém um certificado e uma chave privada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A senha usada para proteger o arquivo especificado por <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Define a versão mínima do servidor necessária para emitir licenças para o conteúdo que está sendo empacotado. Especifique x (Acesso ao Adobe x.0), onde x = o número da versão principal. Servidores anteriores ao Adobe Access 3.0 não oferecem suporte a essa configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se uma política <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> exige o registro de domínio com um servidor que usa um certificado de transporte diferente do especificado em <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, o certificado de transporte de domínio precisa ser fornecido. </p> <p class="- topic/p ">Essa propriedade especifica um arquivo que contém somente o certificado (o formato PEM ou DER é aceitável). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifique a chave de licença. Se nenhuma chave for especificada, ela será gerada aleatoriamente. Quando a rotação de chaves não está ativada, essa é a chave usada para criptografar o conteúdo. </p> <p class="- topic/p ">Quando a rotação de chaves está habilitada, essa chave é usada para proteger as chaves de rotação. A chave deve ter 16 bytes de comprimento e ser especificada como valores hexadecimais. O espaço em branco entre os valores hexadecimais é opcional. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica se a rotação de chaves está habilitada. Se definido como false (padrão), a rotação de chaves é desativada e o CEK principal será usado para criptografar todas as amostras no conteúdo. </p> <p class="- topic/p ">Se definido como verdadeiro, a rotação de chaves será habilitada e chaves diferentes poderão ser usadas para criptografar partes do conteúdo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequência de chaves rotacionadas usada para criptografar o conteúdo quando a rotação de chaves está habilitada. Se nenhuma chave for especificada, as chaves serão geradas aleatoriamente. As chaves devem ter 16 bytes de comprimento e ser especificadas como valores hexadecimais. </p> <p class="- topic/p ">O espaço em branco entre os valores hexadecimais é opcional. <i class="+ topic/ph hi-d/i ">n</i> deve aumentar monotonicamente, a partir de 1. Quando várias chaves forem especificadas, elas serão percorridas na ordem indicada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o intervalo (em segundos) durante o qual uma chave de rotação será usada para criptografar amostras de conteúdo. </p> <p class="- topic/p ">Após esse período de tempo no conteúdo ter sido criptografado, a próxima chave de rotação será usada. Se a rotação de chaves estiver habilitada e nenhum intervalo for especificado, as chaves serão giradas a cada 15 minutos. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se verdadeiro, não há servidor de licença do qual as licenças possam ser obtidas. As licenças devem ser incorporadas ou obtidas fora da faixa. O padrão é falso, se não for especificado. Compatível somente com o Adobe Access Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>
