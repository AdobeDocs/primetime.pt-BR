---
seo-title: Propriedades do arquivo de configuração
title: Propriedades do arquivo de configuração
uuid: f0d36240-e5fa-4bf9-9a82-7e963d03cdd0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Propriedades do arquivo de configuração {#configuration-file-properties}

Antes de executar o Media Packager, especifique os valores para as propriedades do Media Packager. O arquivo de configuração especifica as seguintes propriedades. Para nomes de propriedade que incluem* n*, *n* representa um número inteiro que começa com 1 e aumenta para cada instância da propriedade.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Propriedade </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se o conteúdo do vídeo deve ser criptografado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica se o áudio deve ser criptografado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.script</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se os dados de script devem ser criptografados em FLVs. <i class="+ topic/ph hi-d/i ">As tags de dados </i> onMetaData e  <i class="+ topic/ph hi-d/i "></i> onXMPscript nunca são criptografadas, mesmo se essa opção estiver ativada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica o nível de criptografia do vídeo. Um valor alto é usado para criptografar todo o conteúdo do vídeo, enquanto valores médio e baixo são usados para criptografar partes do conteúdo do vídeo para arquivos F4V que contêm conteúdo H.264. </p> <p class="- topic/p ">value = <span class="codeph"> high | meio | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.secondUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se o valor for maior que 0, o número especificado de segundos de conteúdo no início do arquivo não será criptografado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O arquivo de certificado do servidor de licenças usado para criptografar a chave. A propriedade <span class="codeph"> encrypt.keys.asymmetric.certfile</span> especifica um arquivo que contém somente o certificado (o formato PEM ou DER é aceitável). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Essa propriedade é usada repetidamente para criar uma lista de políticas a serem aplicadas ao conteúdo. <span class="codeph"> é </span> um número inteiro cujo valor é 1 ou maior. O cliente usará a primeira instância por padrão. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O URL do servidor de licenças. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O certificado de transporte do servidor de licenças. Esta propriedade especifica um arquivo <span class="filepath"> .cer</span> que contém somente o certificado (o formato PEM ou DER é aceitável). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O arquivo PKCS12 que contém credenciais de empacotador para assinatura de conteúdo. O <span class="codeph"> encrypt.sign.certfile</span> deve fazer referência a um arquivo <span class="filepath"> .pfx</span> que contém um certificado e uma chave privada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A senha usada para proteger o arquivo especificado por <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Define a versão mínima do servidor necessária para emitir licenças para o conteúdo que está sendo empacotado. Especifique x (Adobe Access x.0), onde x = o número da versão principal. Os servidores anteriores ao Adobe Access 3.0 não suportam essa configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se uma política <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> exigir o registro de domínio com um servidor que utilize um certificado de transporte diferente do especificado em <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, o certificado de transporte de domínio deverá ser fornecido. </p> <p class="- topic/p ">Essa propriedade especifica um arquivo que contém somente o certificado (o formato PEM ou DER é aceitável). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifique a chave de licença. Se nenhuma chave for especificada, a chave será gerada aleatoriamente. Quando a rotação de chaves não está ativada, essa é a chave usada para criptografar o conteúdo. </p> <p class="- topic/p ">Quando a rotação de chaves está ativada, esta tecla é usada para proteger as chaves de rotação. A chave deve ter 16 bytes de comprimento e ser especificada como valores hexadecimais. O espaço em branco entre os valores hexadecimais é opcional. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotativamente.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica se a rotação de chaves está ativada. Se definido como false (padrão), a rotação de chaves será desativada e o CEK principal será usado para criptografar todas as amostras no conteúdo. </p> <p class="- topic/p ">Se definido como true, a rotação de chaves será ativada e chaves diferentes poderão ser usadas para criptografar partes do conteúdo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rots.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequência de chaves giradas usadas para criptografar o conteúdo quando a rotação de chaves está ativada. Se nenhuma chave for especificada, as chaves serão geradas aleatoriamente. As chaves devem ter 16 bytes de comprimento e ser especificadas como valores hexadecimais. </p> <p class="- topic/p ">O espaço em branco entre os valores hexadecimais é opcional. <i class="+ topic/ph hi-d/i ">Não </i> deve aumentar monotonicamente, a partir de 1. Quando várias teclas forem especificadas, as teclas serão percorridas na ordem indicada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.otação.range</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o intervalo (em segundos) durante o qual uma chave de rotação será usada para criptografar amostras de conteúdo. </p> <p class="- topic/p ">Depois que esse tempo no conteúdo for criptografado, a próxima chave de rotação será usada. Se a rotação de chaves estiver ativada e nenhum intervalo for especificado, as chaves serão giradas a cada 15 minutos. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se verdadeiro, não há servidor de licenças do qual as licenças possam ser obtidas. As licenças devem ser incorporadas ou obtidas fora de banda. O padrão é falso se não for especificado. Só é suportado no Adobe Access Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>

