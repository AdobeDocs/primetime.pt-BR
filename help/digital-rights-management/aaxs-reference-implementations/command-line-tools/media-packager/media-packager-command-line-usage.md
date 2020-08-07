---
seo-title: Uso da linha de comando
title: Uso da linha de comando
uuid: 5f24f18d-09ef-400a-9404-50a9fcf4316d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Uso da linha de comando {#command-line-usage}

Antes de usar o Media Packager, verifique se você atende aos requisitos listados em Requisitos e se o arquivo de configuração contém as informações necessárias (consulte Arquivo de configuração em *Uso das implementações* de referência de acesso ao Adobe.

O Media Packager está no [!DNL \Reference Implementation\Command Line tools] diretório do DVD. Para criptografar um único arquivo, use a seguinte sintaxe:

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

* `source` é o arquivo a ser criptografado.
* `dest` especifica onde o conteúdo criptografado será gravado. Se um diretório for especificado, o arquivo criptografado será salvo nessa pasta usando o mesmo nome de arquivo que o arquivo de origem, mas o diretório não deve ser o diretório que contém o arquivo de origem.

Para criptografar vários arquivos com a mesma chave (para suporte à taxa de vários bits), use a seguinte sintaxe:

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

* `sourcefiles` é uma série de entradas de origem delimitadas por espaços em branco que representam os arquivos a serem criptografados.
* `dest-directory` especifica onde o conteúdo criptografado será gravado. Os arquivos criptografados serão salvos nessa pasta usando os mesmos nomes de arquivo que os arquivos de origem, mas o diretório não deve ser o diretório que contém os arquivos de origem.

Para visualização de informações sobre um arquivo criptografado, use a seguinte sintaxe:

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` é o arquivo criptografado.

Para visualização de informações sobre um arquivo de metadados, use a seguinte sintaxe:

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` é um [!DNL .metadata] arquivo que contém os metadados DRM.

>[!NOTE]
>
>Durante o empacotamento, o Media Packager não gerará mais um arquivo .header por padrão. Para gerar esse arquivo, use a `-h` opção durante o empacotamento.

A tabela a seguir contém descrições das opções de linha de comando mostradas na sintaxe acima:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o local do arquivo de configuração. Se essa opção não for usada, o Media Packager procurará por <span class="filepath"> flashaccess stools.properties </span> no diretório de trabalho. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d arquivo <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Mostra informações sobre um arquivo que já foi empacotado. Os arquivos de origem e de destino não são obrigatórios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Mostra informações sobre metadados existentes. Os arquivos de origem e de destino não são obrigatórios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use essa opção com <span class="codeph"> -d </span> para extrair políticas de um arquivo empacotado. Um arquivo será criado no mesmo diretório do arquivo criptografado usando o nome do arquivo e o identificador da política. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use com <span class="codeph"> -d </span> para extrair o cabeçalho DRM de um arquivo empacotado. Um arquivo é criado no mesmo diretório do arquivo criptografado, usando o nome do arquivo e a extensão <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica um identificador exclusivo para este conteúdo. Se nenhum identificador for especificado, o nome do arquivo desfile será usado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> chave </span>= <span class="+ topic/ph pr-d/codeph codeph"> valor </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica uma chave/valor personalizado para adicionar aos metadados do conteúdo. Várias <span class="codeph"> opções de -k </span> podem ser especificadas. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use essa opção com <span class="codeph"> -d </span> para extrair metadados de um arquivo empacotado. Um arquivo será criado no mesmo diretório do arquivo criptografado usando o nome do arquivo e a extensão <span class="codeph"> .metadata </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o </span> não estiver definido, um erro será retornado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Substitui o arquivo de destino sem avisar, se já existir. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p nome <span class="+ topic/ph pr-d/codeph codeph"> do arquivo [domínio-transporte-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica o nome do arquivo que contém a política. Se a política exigir o registro de domínio em um servidor que use um certificado de transporte diferente daquele especificado no arquivo de propriedades, o certificado de transporte de domínio também precisará ser fornecido. </p> <p class="- topic/p ">Várias opções <span class="codeph"> -p </span> podem ser especificadas e o cliente usará a primeira por padrão. Os valores especificados na linha de comando têm prioridade sobre os especificados no arquivo de configuração. </p> </td> 
  </tr> 
 </tbody> 
</table>

