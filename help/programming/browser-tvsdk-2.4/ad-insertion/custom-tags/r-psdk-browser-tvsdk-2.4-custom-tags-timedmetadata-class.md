---
description: Quando o TVSDK do navegador detecta uma tag inscrita na lista de reprodução/manifesto, o reprodutor tenta automaticamente processar a tag e expô-la como um objeto TimedMetadata.
title: Classe de metadados cronometrados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Classe de metadados cronometrados{#timed-metadata-class}

Quando o TVSDK do navegador detecta uma tag inscrita na lista de reprodução/manifesto, o reprodutor tenta automaticamente processar a tag e expô-la como um objeto TimedMetadata.

A variável `TimedMetadata` A classe fornece os seguintes elementos:

<table id="table_5827A0626EDC45F68DC3E7644F3EFF69"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Propriedade </th> 
   <th colname="col02" class="entry"> Tipo </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>type </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>Estes são os tipos de metadados cronometrados: 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG - os metadados cronometrados foram criados a partir de uma tag na lista de reprodução/manifesto. </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 - os metadados cronometrados foram criados de uma tag ID3 no fluxo de mídia. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>hora </p> </td> 
   <td colname="col02"> <p>Número </p> </td> 
   <td colname="col2"> <p>A posição da hora local (milissegundos) em relação ao início do conteúdo principal em que esses metadados cronometrados estão presentes no fluxo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>String </p> </td> 
   <td colname="col2"> <p>O identificador exclusivo dos metadados cronometrados. </p> <p>Normalmente é extraído do atributo cue/tag ID, se presente. Caso contrário, será um valor aleatório exclusivo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>Número </p> </td> 
   <td colname="col2"> <p>O nome dos metadados temporizados. </p> <p>Se o tipo for TAG, o valor representa o nome da sinalização/tag. Se o tipo for ID3, o valor será nulo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>conteúdo </p> </td> 
   <td colname="col02"> <p>String </p> </td> 
   <td colname="col2"> <p>O conteúdo bruto dos metadados cronometrados. </p> <p>Se o tipo for TAG, o valor representa toda a lista de atributos da indicação/tag. Se o tipo id ID3, o valor será nulo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>metadados </p> </td> 
   <td colname="col02"> <p><span class="codeph"> Metadados</span> </p> </td> 
   <td colname="col2"> <p>As informações processadas/extraídas da tag personalizada da lista de reprodução/manifesto. </p> </td> 
  </tr> 
 </tbody> 
</table>
