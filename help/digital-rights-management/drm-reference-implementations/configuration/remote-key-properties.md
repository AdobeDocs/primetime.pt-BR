---
description: nulo
seo-description: nulo
seo-title: Propriedades de entrega de chave remota (iOS)
title: Propriedades de entrega de chave remota (iOS)
uuid: 17e1b756-d106-47a7-99ae-641190693870
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Propriedades de entrega de chave remota (iOS){#remote-key-delivery-properties-ios}

Para suportar a geração de licenças para entrega de chave remota a um cliente iOS no Adobe Primetime DRM, você deve especificar o certificado do servidor de chave no `flashaccess-refimpl.properties` arquivo.

As seguintes propriedades foram adicionadas ao Primetime DRM:

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
   <td colname="2" class="- topic/entry "> <p>Certificado do servidor de licença do servidor de chave emitido pela Adobe. </p> <p>Este certificado gera licenças para dispositivos iOS quando os metadados indicam que um Servidor de chaves é necessário. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>O alias de um certificado do servidor de chave emitido pela Adobe e armazenado em HSM. </p> <p>Ao ativar o HSM, você pode aplicar essa propriedade em vez da propriedade <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> . </p> </td> 
  </tr> 
 </tbody> 
</table>

