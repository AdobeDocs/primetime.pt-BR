---
title: Propriedades de entrega de chave remota (iOS)
description: Propriedades de entrega de chave remota (iOS)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Propriedades de entrega de chave remota (iOS){#remote-key-delivery-properties-ios}

Para dar suporte à geração de licenças para entrega Remota de Chave para um cliente iOS no Adobe Primetime DRM, você deve especificar o certificado do Servidor de Chave no `flashaccess-refimpl.properties` arquivo.

As seguintes propriedades foram adicionadas no Primetime DRM:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Propriedade </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Certificado de servidor de licença do servidor de chave emitido pelo Adobe. </p> <p>Esse certificado gera licenças para dispositivos iOS quando os metadados indicam que um servidor de chaves é necessário. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>O alias de um certificado de servidor de licenças emitido por Adobe do servidor de chaves que está armazenado no HSM. </p> <p>Ao habilitar o HSM, você pode aplicar essa propriedade em vez da variável <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> propriedade. </p> </td> 
  </tr> 
 </tbody> 
</table>
