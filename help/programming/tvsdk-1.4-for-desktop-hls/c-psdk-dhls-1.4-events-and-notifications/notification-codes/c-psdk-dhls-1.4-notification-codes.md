---
description: O sistema de notificação TVSDK produz vários avisos de erro, aviso e informações que fornecem metadados de diagnóstico.
seo-description: O sistema de notificação TVSDK produz vários avisos de erro, aviso e informações que fornecem metadados de diagnóstico.
seo-title: Códigos de notificação
title: Códigos de notificação
uuid: a7b77a5c-9873-45cf-8499-aa00270a7ad6
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Visão geral {#notification-codes-overview}

O sistema de notificação TVSDK produz vários avisos de erro, aviso e informações que fornecem metadados de diagnóstico.

Os objetos de notificação fornecem informações relacionadas ao status do player. O TVSDK fornece uma lista ordenada cronologicamente de objetos de notificação, e cada notificação contém os seguintes metadados:

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Elemento </th> 
   <th colname="2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> type </td> 
   <td colname="2"> O tipo de notificação. Dependendo da plataforma, essa propriedade se refere a um tipo enumerado com possíveis valores de INFO, WARN ou ERROR. Este é o agrupamento de nível superior para notificações. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> código </td> 
   <td colname="2">A representação numérica atribuída à notificação: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Eventos de notificação de erros, de 100000 a 19999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Eventos de notificação de aviso, de 200000 a 29999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Eventos de notificação de informações, de 300000 a 399999 </li> 
    </ul> <p>Cada intervalo de nível superior, como erros, é dividido em subintervalos, como 101000 a 101999 representando erros de reprodução. </p>
    <pre>
     A lista discriminada 
     <span class="codeph"> mediacore.PSDKErrorCode</span> lista os valores possíveis.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> name </td> 
   <td colname="2">Uma string que contém uma descrição legível por humanos do código, como <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> metadados </td> 
   <td colname="2">Pares chave/valor que contêm informações adicionais relevantes sobre a notificação. Por exemplo, uma chave chamada <span class="codeph"> URL</span> seria emparelhada com um valor que é um URL relacionado à notificação, como um URL inválido que causou um erro. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> innerNotification </td> 
   <td colname="2">Uma referência a outro objeto <span class="codeph"> MediaPlayerNotification</span> que afetou diretamente essa notificação. Um exemplo pode ser uma notificação sobre uma falha de inserção de anúncio que corresponde diretamente a um conflito de inserção de linha do tempo. Nem todas as notificações fornecem uma notificação interna. </td> 
  </tr> 
 </tbody> 
</table>

