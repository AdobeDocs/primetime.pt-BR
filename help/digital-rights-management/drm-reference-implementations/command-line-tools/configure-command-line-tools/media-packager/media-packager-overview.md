---
title: Visão geral
description: Visão geral
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# DRM Media Packager {#media-packager}

Uso do Media Packager ( [!DNL AdobePackager.jar]) para especificar uma política de DRM a ser aplicada ao seu conteúdo e para especificar qual parte do conteúdo deve ser criptografada. Por exemplo, você pode especificar que o empacotador deve criptografar os dados de vídeo, mas não os dados de áudio.

Antes de executar [!DNL AdobePackager.jar], defina as propriedades na seção Propriedades do Media Packager do arquivo de configuração.

>[!NOTE]
>
>Você também pode especificar todas as propriedades do Media Packager a partir da linha de comando.

## Uso da linha de comando do Media Packager {#media-packager-command-line-usage}

**Compactar um arquivo:**

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` - O nome do arquivo que você deseja criptografar.
* `dest` - O nome do arquivo criptografado resultante.

  Se você especificar um diretório, o arquivo criptografado será salvo automaticamente no diretório especificado com o mesmo nome de arquivo especificado como o arquivo de origem. No entanto, não é possível especificar um diretório de destino que inclua o arquivo de origem.

**Compactar vários arquivos com a mesma chave** (para suporte a taxa de vários bits):

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` - Uma série de entradas de origem delimitadas por espaços em branco para os arquivos que você deseja criptografar.
* `dest-directory` - O diretório de destino onde você deseja gravar o conteúdo criptografado. Os arquivos criptografados são salvos automaticamente nesse diretório usando os mesmos nomes de arquivo que os arquivos de origem. No entanto, o diretório de destino não pode incluir arquivos de origem.

**Exibir informações sobre um arquivo criptografado:**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**Exibir informações sobre um arquivo de metadados:**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` é um [!DNL .metadata] arquivo que inclui metadados de DRM.

>[!NOTE]
>
>Durante o empacotamento, o Media Packager não pode mais gerar uma [!DNL .header] arquivo por padrão. Para gerar uma [!DNL .header] arquivo, use o `-h` opção durante a embalagem.

**Tabela 3: Opções**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção de linha de comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nome e o local do arquivo de configuração. </p> <p class="- topic/p ">Se você não especificar um nome ou um local, o DRM Media Packager procurará <span class="filepath"> flashaccesstools.properties </span> no diretório de trabalho atual. </p> <p>Observação: As opções especificadas na linha de comando têm prioridade sobre as opções especificadas no arquivo de configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permite exibir informações sobre um arquivo já empacotado. </p> <p class="- topic/p ">Os arquivos de origem e destino não são obrigatórios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> arquivo de metadados </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permite exibir informações sobre metadados existentes. </p> <p class="- topic/p ">Os arquivos de origem e destino não são obrigatórios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extrai políticas DRM de um arquivo empacotado quando você aplica esta opção em conjunto com o <span class="codeph"> -d </span> opção. </p> <p class="- topic/p ">Um arquivo é criado automaticamente no mesmo diretório em que o arquivo criptografado está localizado com um nome de arquivo e um identificador de política DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extrai o cabeçalho DRM de um arquivo empacotado ao aplicar essa opção em conjunto com o <span class="codeph"> -d </span> opção. </p> <p class="- topic/p ">Um arquivo é criado automaticamente no mesmo diretório em que o arquivo criptografado está localizado com o nome e a extensão do arquivo <span class="filepath"> .cabeçalho </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica um identificador exclusivo para este segmento de conteúdo. </p> <p class="- topic/p ">Se você não especificar um identificador, o nome do arquivo de desfile será aplicado automaticamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> value </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica uma chave/valor personalizado para adicionar aos metadados de conteúdo. </p> <p class="- topic/p ">É possível especificar vários <span class="codeph"> -k </span> opções. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extrair metadados de um arquivo empacotado ao aplicar essa opção em conjunto com o <span class="codeph"> -d </span> opção. </p> <p class="- topic/p ">Um arquivo é criado automaticamente no mesmo diretório do arquivo criptografado com um nome de arquivo e um <span class="codeph"> .metadata </span> extensão. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. </p> <p class="- topic/p ">Se o arquivo de destino já existir e <span class="codeph"> -o </span> não estiver definido, ocorrerá um erro. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Substitui o arquivo de destino sem que você seja avisado, a menos que ele já exista. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> filename [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nome do arquivo que inclui a política DRM. </p> <p class="- topic/p ">Se a política DRM exigir registro de domínio com um servidor que use um certificado de transporte diferente daquele especificado no arquivo de propriedades, será necessário fornecer o certificado de transporte do domínio. </p> <p class="- topic/p ">É possível especificar vários <span class="codeph"> -p </span> opções. O cliente sempre aplica a primeira opção por padrão. Os valores especificados na linha de comando têm precedência sobre aqueles especificados no arquivo de configuração. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propriedades de configuração {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>Para nomes de propriedades que incluem* n*, *n* representa um número inteiro que começa com 1 e aumenta para cada instância da propriedade.

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
   <td colname="2" class="- topic/entry "> <p>Indica se os dados de script devem ser criptografados em mp4s. </p> <p><i class="+ topic/ph hi-d/i ">onMetaData</i> e <i class="+ topic/ph hi-d/i ">onXMP</i> as tags de dados de script nunca são criptografadas mesmo se você ativar essa opção. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica o nível de criptografia do vídeo. </p> <p class="- topic/p ">Um valor de <span class="codeph"> alta</span> é usado para criptografar todo o conteúdo de vídeo, enquanto valores de <span class="codeph"> médio</span> e <span class="codeph"> baixa</span> são usados para criptografar partes do conteúdo de vídeo para arquivos mp4 que incluem conteúdo H.264. </p> <p class="- topic/p ">value = <span class="codeph"> alta | médio | baixa</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se um valor for maior que 0, o número especificado de segundos de conteúdo no início do arquivo não será criptografado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O arquivo de certificado do servidor de licenças usado para criptografar a chave. </p> <p class="- topic/p ">A variável <span class="codeph"> encrypt.keys.asymmetric.certfile</span> A propriedade especifica um arquivo que inclui somente o certificado (o formato PEM ou DER é aceitável). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Essa propriedade é usada repetidamente para criar uma lista de políticas de DRM a serem aplicadas ao conteúdo. <span class="codeph"> n</span> representa um número inteiro cujo valor é 1 ou superior. O cliente usa a primeira instância por padrão. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O URL do servidor de licenças </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O certificado de transporte do servidor de licenças. </p> <p class="- topic/p ">Esta propriedade especifica uma <span class="filepath"> .cer</span> arquivo que inclui somente o certificado (o formato PEM ou DER é aceitável). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">O arquivo PKCS12 que inclui credenciais de empacotador para assinatura de conteúdo. </p> <p class="- topic/p ">A variável <span class="codeph"> encrypt.sign.certfile</span> precisa se referir a um <span class="filepath"> .pfx</span> arquivo que inclui um certificado e uma chave privada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A senha que você pode aplicar para proteger o arquivo que foi especificado por <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Define a versão mínima do servidor necessária para emitir licenças para o conteúdo que está sendo empacotado. </p> <p class="- topic/p ">Especifique x (para o Primetime DRM x.0), onde x representa um número de versão principal. Nenhuma versão de servidores anterior ao Adobe Primetime versão 3.0 é compatível com essa configuração. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se uma política DRM <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> exige o registro de domínio com um servidor que ofereça suporte a um certificado de transporte diferente daquele que você especificou em <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, é necessário fornecer as necessidades de certificado de transporte de domínio. </p> <p class="- topic/p ">Essa propriedade especifica um arquivo que inclui somente o certificado (o formato PEM ou DER é aceitável). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica uma chave de licença. </p> <p class="- topic/p ">Se você não especificar uma chave, ela será gerada aleatoriamente. Quando você não ativa a rotação de chaves, pode usar essa chave para criptografar o conteúdo. </p> <p class="- topic/p ">Ao ativar a rotação de chaves, você pode usá-la para proteger as chaves de rotação. A chave deve ter 16 bytes de comprimento e ser especificada como valores hexadecimais. O espaço em branco entre os valores hexadecimais é opcional. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica se a rotação de chaves está habilitada. </p> <p class="- topic/p ">Se definida como false, que é a configuração padrão, a rotação de chaves é desativada e o CEK principal é usado para criptografar todas as amostras no conteúdo. </p> <p class="- topic/p ">Se definido como verdadeiro, a rotação de chaves é habilitada e chaves diferentes podem ser usadas para criptografar segmentos de qualquer conteúdo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequência de chaves giradas que você pode especificar para criptografar o conteúdo quando a rotação de chaves estiver ativada. </p> <p class="- topic/p ">Se você não especificar nenhuma chave, as chaves serão geradas aleatoriamente. As chaves devem ter 16 bytes de comprimento e ser especificadas como valores hexadecimais. </p> <p class="- topic/p ">O espaço em branco entre os valores hexadecimais é opcional. <i class="+ topic/ph hi-d/i ">n</i> deve aumentar monotonicamente, a partir de 1. Ao especificar várias teclas, elas são percorridas na ordem indicada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o intervalo em segundos durante o qual você pode aplicar uma chave de rotação para criptografar amostras de conteúdo. </p> <p class="- topic/p ">Após o intervalo de tempo em que o conteúdo foi criptografado, a próxima chave de rotação é aplicada. Se você tiver ativado a rotação de chaves, mas não tiver especificado nenhum intervalo de tempo, as chaves serão automaticamente rotacionadas a cada 15 minutos. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se essa opção estiver definida como true, então um servidor de licença do qual as licenças podem ser obtidas não estará disponível. </p> <p class="- topic/p ">As licenças devem ser incorporadas ou obtidas fora da faixa. O valor padrão é definido como falso, a menos que você especifique um valor diferente. Essa opção só é compatível com o Primetime DRM Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>
