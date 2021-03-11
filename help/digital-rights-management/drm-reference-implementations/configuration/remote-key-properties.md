---
title: Propriedades do delivery de chave remota (iOS)
description: Propriedades do delivery de chave remota (iOS)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Propriedades de entrega de chave remota (iOS){#remote-key-delivery-properties-ios}

Para suportar a geração de licenças para entrega de chave remota para um cliente iOS no Adobe Primetime DRM , você deve especificar o certificado do Servidor de chaves no arquivo `flashaccess-refimpl.properties` .

As seguintes propriedades foram adicionadas no DRM do Primetime :

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
   <td colname="2" class="- topic/entry "> <p>Certificado do Servidor de Licenças do Servidor de Chave emitido pelo Adobe. </p> <p>Este certificado gera licenças para dispositivos iOS quando os metadados indicam que um Servidor de chaves é necessário. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>O alias de um certificado do Servidor de Licenças emitido por Adobe do Servidor de Chave armazenado no HSM. </p> <p>Ao ativar o HSM, você pode aplicar essa propriedade em vez da propriedade <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </p> </td> 
  </tr> 
 </tbody> 
</table>

