---
title: Uso da linha de comando
description: Uso da linha de comando
copied-description: true
exl-id: 241849bb-e818-420e-98b4-c12e306b17b2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Uso da linha de comando {#command-line-usage}

Para gerar uma licença, use a seguinte sintaxe:

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` é um arquivo .metadata que contém os metadados de DRM de acesso ao Adobe. Esse arquivo pode ser obtido de um conteúdo protegido usando o `-d -m` opção do Media Packager.

Para exibir uma licença gerada anteriormente, use a seguinte sintaxe:

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` é um arquivo que contém uma licença de Acesso Adobe gerada pelo Gerador de Licenças.

A tabela a seguir descreve as opções de linha de comando que podem ser especificadas com a sintaxe mencionada anteriormente:

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
   <td colname="2" class="- topic/entry "> Especifique o local do arquivo de configuração. Se essa opção não for usada, o Gerador de Licenças procurará flashaccesstools.properties no diretório de trabalho. As opções especificadas na linha de comando têm precedência sobre as presentes no arquivo de configuração. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> arquivo de licença</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Mostrar informações sobre uma licença já gerada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf-leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Gere uma licença folha e grave a saída em um arquivo especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m nome do arquivo de metadados</span> </td> 
   <td colname="2" class="- topic/entry "> Especifique os metadados de conteúdo para os quais gerar uma licença. (Obrigatório para gerar a licença) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o</span> não estiver definido, um erro será retornado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, substitua-o sem avisar. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> Se os metadados contiverem várias políticas, especifique o número da política a ser usada (começando em 1) para gerar a licença. Se não for especificado, a primeira política será usada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">Gera uma licença para o recipient especificado. Um dispositivo ou certificado de domínio pode ser usado. Múltiplo <span class="+ topic/ph pr-d/codeph codeph"> -r </span>podem ser especificadas opções para criar uma licença para vários destinatários. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root nome-do-arquivo</span> </td> 
   <td colname="2" class="- topic/entry "> Gera uma licença raiz e grava a saída no arquivo especificado. </td> 
  </tr> 
 </tbody> 
</table>
