---
description: Você pode configurar um controle da interface do usuário para o volume de som.
title: Fornecer controle de volume
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Fornecer controle de volume{#provide-volume-control}

Você pode configurar um controle da interface do usuário para o volume de som.

1. Aguarde até que a instância MediaPlayer esteja em um status válido para esse comando.

   Qualquer estado, exceto LIBERADO, é válido.
1. Chame o método de conjunto de volumes na instância `MediaPlayer` para definir o volume de áudio.

   ```
   public function set volume(value:Number):void
   ```

   O valor do volume representa o volume solicitado expresso em proporção do volume máximo, em que 0 é silencioso e 1 é o volume máximo.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Se o volume especificado for </th> 
      <th colname="col2" class="entry"> O volume resultante é </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> Menos de 0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Entre 0 e 1 </td> 
      <td colname="col2"> O volume especificado </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Maior que 1 </td> 
      <td colname="col2"> O valor dividido por 100 e definido como um dos seguintes valores: 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">O resultado se estiver entre 0 e 1 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 se o resultado for maior que 1 </li> 
      </ul> <p>Dica:  Essa lógica manipula valores que são fornecidos pelos clientes com base em versões anteriores do 
      <span class="codeph">frases/primetime-sdk-name</span>, onde os valores de volume variavam de 0 a 100. </p> </td> 
   </tr> 
   </tbody> 
   </table>
