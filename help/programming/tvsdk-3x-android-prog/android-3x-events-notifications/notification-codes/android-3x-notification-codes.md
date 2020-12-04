---
description: O sistema de notificação TVSDK produz vários avisos de erro, aviso e informações que fornecem metadados de diagnóstico.
seo-description: O sistema de notificação TVSDK produz vários avisos de erro, aviso e informações que fornecem metadados de diagnóstico.
seo-title: Códigos de notificação
title: Códigos de notificação
uuid: 6babb203-b6d4-4b11-9fae-41e7db7fd570
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Códigos de notificação {#notification-codes}

O sistema de notificação TVSDK produz vários avisos de erro, aviso e informações que fornecem metadados de diagnóstico.

Os objetos de notificação fornecem informações relacionadas ao status do player. O TVSDK fornece uma lista classificada cronologicamente de objetos de notificação. Cada notificação contém os seguintes metadados:

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> Elemento</b></th> 
   <th colname="2" class="entry"><b> Descrição</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>O tipo de notificação. </p> <p>Dependendo da plataforma, essa propriedade é um tipo enumerado com possíveis valores de INFO, WARN e ERROR. Este é o agrupamento de nível superior para notificações. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> código</span> </td> 
   <td colname="2"> <p>As seguintes representações numéricas são atribuídas às notificações: 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">Eventos de notificação de erros, de 100000 a 19999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">Eventos de notificação de aviso, de 200000 a 29999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">Eventos de notificação de informações, de 300000 a 399999 </li> 
     </ul> </p> <p>Cada intervalo de nível superior, como erros, é dividido em subintervalos, como 101000 a 101999 representando erros de reprodução. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Uma string que contém uma descrição legível por humanos do evento de notificação, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadados</span> </td> 
   <td colname="2"> <p>Pares chave/valor que contêm informações adicionais relevantes sobre a notificação. </p> <p>Por exemplo, uma chave chamada <span class="codeph"> URL</span> forneceria um valor que é um URL relacionado à notificação, como um URL inválido que causou um erro. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>Uma referência a outro objeto <span class="codeph"> MediaPlayerNotification</span> que afetou diretamente essa notificação. </p> <p>Um exemplo pode ser uma notificação sobre uma falha de inserção de anúncio que corresponde diretamente a um conflito de inserção de linha do tempo. Nem todas as notificações fornecem uma notificação interna. </p> </td> 
  </tr> 
 </tbody> 
</table>