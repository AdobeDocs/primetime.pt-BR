---
seo-title: Uso da linha de comando
title: Uso da linha de comando
uuid: b3a995de-653e-491a-9262-86dc56b9ce31
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '0'
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

`metadata` é um arquivo .metadata que contém os metadados DRM de Adobe Access. Esse arquivo pode ser obtido de conteúdo protegido usando a opção `-d -m` do Media Packager.

Para exibir uma licença gerada anteriormente, use a seguinte sintaxe:

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` é um arquivo que contém uma licença de Adobe Access gerada pelo Gerador de licenças.

A tabela a seguir descreve as opções de linha de comando que podem ser especificadas junto com a sintaxe mencionada anteriormente:

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
   <td colname="2" class="- topic/entry "> Especifique o local do arquivo de configuração. Se essa opção não for usada, o Gerador de Licenças procurará flashaccess.properties no diretório de trabalho. As opções especificadas na linha de comando têm prioridade sobre as presentes no arquivo de configuração. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> arquivo licenciado</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Mostrar informações sobre uma licença que já foi gerada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-folha de nome de arquivo</span> </td> 
   <td colname="2" class="- topic/entry "> Gere uma licença de folha e grave a saída em um arquivo especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Especifique os metadados de conteúdo para os quais gerar uma licença. (Obrigatório para gerar licença) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Não pergunte se o arquivo de destino deve ser substituído. Se o arquivo de destino já existir e <span class="codeph"> -o</span> não estiver definido, um erro será retornado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se o arquivo de destino já existir, substitua-o sem solicitar. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> Se os metadados contiverem várias políticas, especifique o número da política a ser usada (começando em 1) para gerar a licença. Se não for especificado, a primeira política será usada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r certificado de recipient</span> </td> 
   <td colname="2" class="- topic/entry ">Gere uma licença para o recipient especificado. Um dispositivo ou certificado de domínio pode ser usado. Várias <span class="+ topic/ph pr-d/codeph codeph"> -r </span>opções podem ser especificadas para criar uma licença para vários recipient. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Gere uma licença raiz e grave a saída no arquivo especificado. </td> 
  </tr> 
 </tbody> 
</table>

