---
description: A Qualidade do serviço (QoS) oferece uma visualização detalhada do desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
title: Rastrear no nível do fragmento usando informações de carregamento
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Rastrear no nível do fragmento usando informações de carregamento{#track-at-the-fragment-level-using-load-information}

A Qualidade do serviço (QoS) oferece uma visualização detalhada do desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.

O TVSDK também fornece informações sobre os seguintes recursos baixados:

1. Arquivos de lista de reprodução/manifesto
1. Fragmentos de arquivo
1. Informações de rastreamento para arquivos

   Você pode ler informações de qualidade de serviço (QoS) sobre recursos baixados, como fragmentos e rastreamentos, no `LoadInfo` classe.

1. Implementar o `onLoadInfo` ouvinte de eventos de retorno de chamada.
1. Registre o ouvinte de eventos, que o TVSDK chama sempre que um fragmento é baixado.
1. Leia os dados de interesse no `LoadInfo` que é passado para o retorno de chamada.

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
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
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> <p>A duração do download em milissegundos. </p> <p>O TVSDK não diferencia entre o tempo necessário para o cliente se conectar ao servidor e o tempo necessário para baixar o fragmento completo. Por exemplo, se um segmento de 10 MB levar 8 segundos para baixar, o TVSDK fornecerá essas informações, mas não informará que levou 4 segundos até o primeiro byte e outros 4 segundos para baixar o fragmento inteiro. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> A duração da mídia dos fragmentos baixados em milissegundos. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> O índice de período da linha do tempo associado ao recurso baixado. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> tamanho </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> O tamanho do recurso baixado em bytes. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> O índice da faixa correspondente, se conhecido; caso contrário, 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <span class="codeph"> String </span> </td> 
      <td colname="col2"> O nome da faixa correspondente, se for conhecido; caso contrário, é nulo. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <span class="codeph"> String </span> </td> 
      <td colname="col2"> O tipo da faixa correspondente, se conhecida; caso contrário, é nulo. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <span class="codeph"> String </span> </td> 
      <td colname="col2"> O que o TVSDK baixou. Uma das seguintes opções: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFESTO - Uma lista de reprodução/manifesto </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAGMENTO - Um fragmento </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">RASTREAR - Um fragmento associado a uma faixa específica </li> 
      </ul> Às vezes, pode não ser possível detectar o tipo do recurso. Se isso ocorrer, FILE será retornado. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <span class="codeph"> String </span> </td> 
      <td colname="col2"> O URL que aponta para o recurso baixado. </td> 
      </tr> 
    </tbody> 
   </table>
