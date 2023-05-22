---
description: Você pode ler informações de qualidade de serviço (QoS) sobre recursos baixados, como fragmentos e rastreamentos, a partir da classe LoadInformation.
title: Rastrear no nível do fragmento usando informações de carregamento
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# Rastrear no nível do fragmento usando informações de carregamento{#track-at-the-fragment-level-using-load-information}

Você pode ler informações de qualidade de serviço (QoS) sobre recursos baixados, como fragmentos e rastreamentos, a partir da classe LoadInformation.

1. Implementar o `onLoadInformationAvailable` ouvinte de eventos de retorno de chamada.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. Registre o ouvinte de eventos, que o TVSDK chama sempre que um fragmento é baixado.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. Leia os dados de interesse no `LoadInformation` que é passado para o retorno de chamada.

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> Propriedade </th> 
      <th colname="col1" class="entry"> Tipo </th> 
      <th colname="col2" class="entry"> Descrição </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> <p>A duração do download em milissegundos. </p> <p>O TVSDK não diferencia entre o tempo necessário para o cliente se conectar ao servidor e o tempo necessário para baixar o fragmento completo. Por exemplo, se um segmento de 10 MB levar 8 segundos para baixar, o TVSDK fornecerá essas informações, mas não informará que levou 4 segundos até o primeiro byte e outros 4 segundos para baixar o fragmento inteiro. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> A duração da mídia dos fragmentos baixados em milissegundos. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> tamanho </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> O tamanho do recurso baixado em bytes. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> O índice da faixa correspondente, se conhecido; caso contrário, 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O nome da faixa correspondente, se for conhecido; caso contrário, é nulo. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O tipo da faixa correspondente, se conhecida; caso contrário, é nulo. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O que o TVSDK baixou. Uma das seguintes opções: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFESTO - Uma lista de reprodução/manifesto </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAGMENTO - Um fragmento </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">RASTREAR - Um fragmento associado a uma faixa específica </li> 
      </ul> Às vezes, pode não ser possível detectar o tipo do recurso. Se isso ocorrer, FILE será retornado. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O URL que aponta para o recurso baixado. </td> 
   </tr> 
   </tbody> 
   </table>
