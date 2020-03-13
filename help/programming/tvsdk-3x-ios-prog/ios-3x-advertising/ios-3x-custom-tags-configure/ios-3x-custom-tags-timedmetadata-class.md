---
description: Quando o TVSDK detecta uma tag assinada na lista de reprodução/manifesto, o player tenta automaticamente processar a tag e expô-la na forma de um objeto PTTimedMetadata.
seo-description: Quando o TVSDK detecta uma tag assinada na lista de reprodução/manifesto, o player tenta automaticamente processar a tag e expô-la na forma de um objeto PTTimedMetadata.
seo-title: Classe de metadados cronometrados
title: Classe de metadados cronometrados
uuid: d76b2a6b-2995-4559-b15d-82ded4c27eea
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Classe de metadados cronometrados {#timed-metadata-class}

Quando o TVSDK detecta uma tag assinada na lista de reprodução/manifesto, o player tenta automaticamente processar a tag e expô-la na forma de um objeto PTTimedMetadata.

A classe fornece os seguintes elementos:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Propriedade</b></th> 
   <th colname="col02" class="entry"><b>Tipo</b> </th> 
   <th colname="col2" class="entry"><b>Descrição</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadataId</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span> </td> 
   <td colname="col2"> Identificador exclusivo dos metadados cronometrados. Normalmente, esse valor é extraído do atributo da ID da tag/cue. Caso contrário, um valor aleatório exclusivo será fornecido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span></td> 
   <td colname="col2"> O nome dos metadados cronometrados. Se o tipo for <span class="codeph"> TAG</span>, o valor representará o nome da indicação/tag. Se o tipo for <span class="codeph"> ID3</span>, será nulo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> time</span> </td> 
   <td colname="col02"><span class="codeph"> CMTime</span></td> 
   <td colname="col2"> A posição de tempo, em milissegundos, em relação ao início do conteúdo principal no qual os metadados cronometrados estão presentes no fluxo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> <span class="codeph"> PTTimedMetadataType</span></td> 
   <td colname="col2">O tipo de metadados cronometrados. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG - indica que os metadados cronometrados foram criados a partir de uma tag na lista de reprodução/manifesto. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - indica que os metadados cronometrados foram criados a partir de uma tag ID3 no fluxo de mídia. </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Lembre-se do seguinte:

* O TVSDK extrai automaticamente a lista de atributos em pares de valores chave e armazena os atributos na propriedade de metadados.

   >[!TIP]
   >
   >Dados complexos em tags personalizadas no manifesto, como strings com caracteres especiais, devem estar entre aspas. Por exemplo:   >
   >
   >
   ```>
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```  >
   >



* Se a extração falhar devido a um formato de tag personalizado, a propriedade content sempre conterá os dados brutos da tag, que é a string após dois pontos. Nenhum erro é emitido nesse caso.

| **Elemento** | **Descrição** |
|---|---|
| TAG, ID3 | Tipos possíveis para os metadados cronometrados. |
| `@property (nonatomic, assign) CMTime time` | A posição de tempo, em relação ao início do conteúdo principal, em que esses metadados foram inseridos no fluxo. |
| `@property (nonatomic, assign) PTTimedMetadataType type` | Retorna o tipo de metadados cronometrados. |
| `@property (nonatomic, retain) NSString *metadataId` | Retorna a ID extraída dos atributos de sinalização/tag. Caso contrário, um valor aleatório exclusivo será fornecido. |
| `@property (nonatomic, retain) NSString *name` | Retorna o nome da indicação, que geralmente é o nome da tag HLS. |