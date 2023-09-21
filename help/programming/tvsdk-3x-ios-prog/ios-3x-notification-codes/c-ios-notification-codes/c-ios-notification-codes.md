---
description: O sistema de notificação TVSDK produz vários avisos de erro, aviso e informativos que fornecem metadados de diagnóstico.
title: Sistema de notificação TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Sistema de notificação TVSDK {#tvsdk-notification-system}

O sistema de notificação TVSDK produz vários avisos de erro, aviso e informativos que fornecem metadados de diagnóstico.

Os objetos de notificação fornecem informações relacionadas ao status do player. O TVSDK fornece uma lista classificada cronologicamente de objetos de notificação e cada notificação contém os seguintes metadados:

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Elemento </th> 
   <th colname="2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> O tipo de notificação. Dependendo da plataforma, essa propriedade se refere a um tipo enumerado com valores possíveis de INFO, WARN ou ERROR. Este é o agrupamento de nível superior para notificações. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> código</span> </td> 
   <td colname="2">A representação numérica atribuída à notificação. 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Eventos de notificação de erro, de 100000 a 199999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Eventos de notificação de aviso, de 200000 a 299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Eventos de notificação de informações, de 300000 a 399999 </li> 
    </ul> <p>Cada intervalo de nível superior, como erros, é dividido em subintervalos, como 101000 a 101999, que representam erros de reprodução. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">Uma string que contém uma descrição legível do código, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadados</span> </td> 
   <td colname="2">Pares de chave/valor que contêm informações adicionais relevantes sobre a notificação. Por exemplo, uma chave chamada <span class="codeph"> URL</span> seria emparelhado com um valor que é um URL relacionado à notificação, como um URL inválido que causou um erro. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2">Uma referência a outro <span class="codeph"> PTNotification</span> objeto que afetou diretamente esta notificação. Um exemplo pode ser uma notificação sobre uma falha de inserção de anúncio que corresponde diretamente a um conflito de inserção de linha do tempo. Nem todas as notificações fornecem uma notificação interna. </td> 
  </tr> 
 </tbody> 
</table>
