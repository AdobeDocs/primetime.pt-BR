---
description: A Qualidade do serviço (QoS) oferece uma visualização detalhada sobre o desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
title: Rastrear no nível do fragmento usando informações de carga
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Rastrear no nível do fragmento usando informações de carga{#track-at-the-fragment-level-using-load-information}

A Qualidade do serviço (QoS) oferece uma visualização detalhada sobre o desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.

O TVSDK também fornece informações sobre os seguintes recursos baixados:

1. Arquivos Playlist/manifest
1. Fragmentos de arquivo
1. Rastreamento de informações para arquivos

   Você pode ler informações de qualidade do serviço (QoS) sobre os recursos baixados, como fragmentos e rastreamentos, da classe `LoadInfo`.

1. Implemente o ouvinte de evento de retorno de chamada `onLoadInfo`.
1. Registre o ouvinte de eventos, que o TVSDK chama sempre que um fragmento for baixado.
1. Leia os dados de interesse do parâmetro `LoadInfo` que é passado para o retorno de chamada.

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
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> <p>A duração do download em milissegundos. </p> <p>O TVSDK não diferencia entre o tempo que o cliente levou para se conectar ao servidor e o tempo que levou para baixar o fragmento completo. Por exemplo, se um segmento de 10 MB levar 8 segundos para ser baixado, o TVSDK fornece essas informações, mas não informa que levou 4 segundos até o primeiro byte e outros 4 segundos para baixar o fragmento inteiro. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> A duração da mídia dos fragmentos baixados em milissegundos. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> O índice do período da linha do tempo associado ao recurso baixado. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> size  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> O tamanho do recurso baixado em bytes. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> O índice da via correspondente, se conhecido; caso contrário, 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <span class="codeph"> String  </span> </td> 
      <td colname="col2"> O nome da via correspondente, se conhecido; caso contrário, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <span class="codeph"> String  </span> </td> 
      <td colname="col2"> O tipo da via correspondente, se conhecida; caso contrário, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <span class="codeph"> String  </span> </td> 
      <td colname="col2"> O que TVSDK baixou. Um dos seguintes: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST - Uma lista de reprodução/manifesto </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAGMENTO - Um fragmento </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK - Um fragmento associado a um rastreamento específico </li> 
      </ul> Às vezes, pode não ser possível detectar o tipo do recurso. Se isso ocorrer, FILE será retornado. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <span class="codeph"> String  </span> </td> 
      <td colname="col2"> O URL que aponta para o recurso baixado. </td> 
      </tr> 
    </tbody> 
   </table>
