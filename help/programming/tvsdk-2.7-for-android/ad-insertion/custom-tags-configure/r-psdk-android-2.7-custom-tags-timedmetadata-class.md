---
description: Quando o TVSDK detecta uma tag inscrita na lista de reprodução/manifesto, o reprodutor tenta automaticamente processar e expor a tag na forma de um objeto TimedMetadata.
title: Classe de metadados cronometrados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Classe de metadados cronometrados {#timed-metadata-class}

Quando o TVSDK detecta uma tag inscrita na lista de reprodução/manifesto, o reprodutor tenta automaticamente processar e expor a tag na forma de um objeto TimedMetadata.

A classe fornece os seguintes elementos:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Propriedade </th> 
   <th colname="col02" class="entry"> Tipo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>Identificador exclusivo dos metadados cronometrados. </p> <p>Normalmente, esse valor é extraído do atributo de ID de indicação/tag. Caso contrário, um valor aleatório exclusivo será fornecido. Uso <span class="codeph"> getId </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadados </span> </td> 
   <td colname="col02"> Metadados </td> 
   <td colname="col2"> <p>As informações processadas/extraídas da tag personalizada da lista de reprodução/manifesto. Uso <span class="codeph"> getMetadata </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> String </td> 
   <td colname="col2"> <p>O nome dos metadados temporizados. Se o tipo for <span class="codeph"> TAG </span>, o valor representa o nome da sinalização/tag. Se o tipo for <span class="codeph"> ID3 </span>, é nulo. Uso <span class="codeph"> getName </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> hora </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>A posição de tempo, em milissegundos, relativa ao início do conteúdo principal em que esses metadados cronometrados estão presentes no fluxo. Uso <span class="codeph"> getTime </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> Tipo </td> 
   <td colname="col2"> <p>O tipo de metadados cronometrados. Uso <span class="codeph"> getType </span>. 
     <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
      <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG - indica que os metadados cronometrados foram criados a partir de uma tag na lista de reprodução/manifesto. </li> 
      <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - indica que os metadados cronometrados foram criados de uma tag ID3 no fluxo de mídia. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Lembre-se do seguinte:

* O TVSDK extrai automaticamente a lista de atributos em pares de valores chave e armazena os atributos na propriedade de metadados.

  >[!TIP]
  >
  >Dados complexos em tags personalizadas no manifesto, como cadeias de caracteres com caracteres especiais, devem estar entre aspas. Por exemplo:
  >
  >```
  >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url= 
  >"www.example.com:8090?parameter1=xyz&parameter2=abc"
  >```
  >

* Se a extração falhar devido a um formato de tag personalizado, a propriedade de metadados estará vazia e seu aplicativo deverá extrair as informações reais. Nesse caso, nenhum erro é lançado.

<table id="table_1BAE98BF23F641A3A5709EBE37B327F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Tipo de enumeração pública {TAG, ID3} </span> </td> 
   <td colname="col2"> <p>Possíveis tipos para os metadados cronometrados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public TimedMetadata(Tipo, tempo longo, id longo, Nome da string, Metadados de metadados); </span> </td> 
   <td colname="col2"> <p>Construtor padrão (o tempo é o tempo de transmissão local). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getTime(); </span> </td> 
   <td colname="col2"> <p>A posição de tempo, relativa ao início do conteúdo principal, em que esses metadados foram inseridos no fluxo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Metadados públicos getMetadata(); </span> </td> 
   <td colname="col2"> <p>Os metadados inseridos no fluxo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Type getType(); </span> </td> 
   <td colname="col2"> <p>Retorna o tipo de metadados cronometrados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getId(); </span> </td> 
   <td colname="col2"> <p>Retorna a ID extraída dos atributos cue/tag. Caso contrário, um valor aleatório exclusivo será fornecido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> cadeia de caracteres pública getName(); </span> </td> 
   <td colname="col2"> <p>Retorna o nome da indicação, que geralmente é o nome da tag HLS. </p> </td> 
  </tr> 
 </tbody> 
</table>
