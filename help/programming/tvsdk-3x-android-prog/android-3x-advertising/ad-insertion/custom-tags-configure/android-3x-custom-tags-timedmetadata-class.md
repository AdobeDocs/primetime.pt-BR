---
description: Quando o TVSDK detecta uma tag assinada na lista de reprodução/manifesto, o player tenta automaticamente processar e expor a tag na forma de um objeto TimedMetadata.
seo-description: Quando o TVSDK detecta uma tag assinada na lista de reprodução/manifesto, o player tenta automaticamente processar e expor a tag na forma de um objeto TimedMetadata.
seo-title: Classe de metadados cronometrados
title: Classe de metadados cronometrados
uuid: c7b1c1d7-48b3-43c7-aa21-f800d894976d
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Classe de metadados cronometrados {#timed-metadata-class}

Quando o TVSDK detecta uma tag assinada na lista de reprodução/manifesto, o player tenta automaticamente processar e expor a tag na forma de um objeto TimedMetadata.

A classe fornece os seguintes elementos:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b> Arte </b></th> 
   <th colname="col02" class="entry"> <b> Tipo </b></th> 
   <th colname="col2" class="entry"> <b> Descrição </b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>Identificador exclusivo dos metadados cronometrados. </p> <p>Normalmente, esse valor é extraído do atributo da ID da tag/cue. Caso contrário, um valor aleatório exclusivo será fornecido. Use <span class="codeph"> getId </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadados </span> </td> 
   <td colname="col02"> Metadados </td> 
   <td colname="col2"> <p>As informações processadas/extraídas da tag personalizada playlist/manifest. Use <span class="codeph"> getMetadata </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> String </td> 
   <td colname="col2"> <p>O nome dos metadados cronometrados. Se o tipo for <span class="codeph"> TAG </span>, o valor representa o nome da indicação/tag. Se o tipo for <span class="codeph"> ID3 </span>, será nulo. Use <span class="codeph"> getName </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> time </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>A posição de tempo, em milissegundos, em relação ao start do conteúdo principal no qual os metadados cronometrados estão presentes no fluxo. Use <span class="codeph"> getTime </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> Tipo </td> 
   <td colname="col2"> <p>O tipo de metadados cronometrados. Use <span class="codeph"> getType </span>. 
     <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
      <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG - indica que os metadados cronometrados foram criados a partir de uma tag na lista de reprodução/manifesto. </li> 
      <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - indica que os metadados cronometrados foram criados a partir de uma tag ID3 no fluxo de mídia. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Lembre-se do seguinte:

* O TVSDK extrai automaticamente a lista de atributos em pares de valores chave e armazena os atributos na propriedade de metadados.

   >[!TIP]
   >
   >Dados complexos em tags personalizadas no manifesto, como strings com caracteres especiais, devem estar entre aspas. Por exemplo:
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url= 
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* Se a extração falhar devido a um formato de tag personalizado, a propriedade metadata ficará vazia e seu aplicativo deverá extrair as informações reais. Nesse caso, nenhum erro é emitido.

<table id="table_1BAE98BF23F641A3A5709EBE37B327F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Elemento </b></th> 
   <th colname="col2" class="entry"> <b>Descrição</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public enum Type {TAG, ID3} </span> </td> 
   <td colname="col2"> <p>Tipos possíveis para os metadados cronometrados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public TimedMetadata(tipo, longo tempo, longa ID, nome da cadeia de caracteres, metadados de metadados); </span> </td> 
   <td colname="col2"> <p>Construtor padrão (tempo é o tempo de fluxo local). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getTime(); </span> </td> 
   <td colname="col2"> <p>A posição de tempo, relativa ao start do conteúdo principal, em que esses metadados foram inseridos no fluxo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Metadata getMetadata(); </span> </td> 
   <td colname="col2"> <p>Os metadados inseridos no fluxo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Type getType(); </span> </td> 
   <td colname="col2"> <p>Retorna o tipo de metadados cronometrados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getId(); </span> </td> 
   <td colname="col2"> <p>Retorna a ID extraída dos atributos de sinalização/tag. Caso contrário, um valor aleatório exclusivo será fornecido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public String getName(); </span> </td> 
   <td colname="col2"> <p>Retorna o nome da indicação, que geralmente é o nome da tag HLS. </p> </td> 
  </tr> 
 </tbody> 
</table>