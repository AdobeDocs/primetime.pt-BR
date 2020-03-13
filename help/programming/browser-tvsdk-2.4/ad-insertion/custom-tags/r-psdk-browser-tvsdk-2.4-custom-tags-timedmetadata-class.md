---
description: Quando o TVSDK do navegador detecta uma tag assinada na lista de reprodução/manifesto, o player tenta automaticamente processar a tag e expô-la como um objeto TimedMetadata.
seo-description: Quando o TVSDK do navegador detecta uma tag assinada na lista de reprodução/manifesto, o player tenta automaticamente processar a tag e expô-la como um objeto TimedMetadata.
seo-title: Classe de metadados cronometrados
title: Classe de metadados cronometrados
uuid: 3f276618-5f61-4b41-bd2d-78e7f32178d9
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Classe de metadados cronometrados{#timed-metadata-class}

Quando o TVSDK do navegador detecta uma tag assinada na lista de reprodução/manifesto, o player tenta automaticamente processar a tag e expô-la como um objeto TimedMetadata.

A `TimedMetadata` classe fornece os seguintes elementos:

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
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 - os metadados cronometrados foram criados a partir de uma tag ID3 no fluxo de mídia. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>time </p> </td> 
   <td colname="col02"> <p>Número </p> </td> 
   <td colname="col2"> <p>A posição de hora local (milissegundos) relativa ao início do conteúdo principal no qual os metadados cronometrados estão presentes no fluxo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>String </p> </td> 
   <td colname="col2"> <p>O identificador exclusivo dos metadados cronometrados. </p> <p>Geralmente é extraído do atributo de ID da tag/sinalização, se houver. Caso contrário, é um valor aleatório exclusivo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>Número </p> </td> 
   <td colname="col2"> <p>O nome dos metadados cronometrados. </p> <p>Se o tipo for TAG, o valor representa o nome da marca/indicação. Se o tipo for ID3, o valor será nulo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>conteúdo </p> </td> 
   <td colname="col02"> <p>String </p> </td> 
   <td colname="col2"> <p>O conteúdo bruto dos metadados cronometrados. </p> <p>Se o tipo for TAG, o valor representará a lista inteira de atributos da indicação/tag. Se a ID do tipo ID3, o valor será nulo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>metadados </p> </td> 
   <td colname="col02"> <p><span class="codeph"> Metadados</span> </p> </td> 
   <td colname="col2"> <p>As informações processadas/extraídas da tag personalizada playlist/manifest. </p> </td> 
  </tr> 
 </tbody> 
</table>

