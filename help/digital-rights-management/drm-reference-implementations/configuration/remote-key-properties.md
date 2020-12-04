---
description: nulo
seo-description: nulo
seo-title: Propriedades do delivery da chave remota (iOS)
title: Propriedades do delivery da chave remota (iOS)
uuid: 17e1b756-d106-47a7-99ae-641190693870
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Propriedades do delivery da chave remota (iOS){#remote-key-delivery-properties-ios}

Para suportar a geração de licenças para o delivery de chave remota para um cliente iOS no Adobe Primetime DRM, você deve especificar o certificado do servidor de chave no arquivo `flashaccess-refimpl.properties`.

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
   <td colname="2" class="- topic/entry "> <p>Certificado de servidor de licença do servidor de chave emitido pelo Adobe. </p> <p>Este certificado gera licenças para dispositivos iOS quando os metadados indicam que um Servidor de chaves é necessário. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>O alias de um certificado do Servidor de Licenças emitido por Adobe do Servidor de Chave que está armazenado no HSM. </p> <p>Ao ativar o HSM, você pode aplicar essa propriedade em vez da propriedade <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </p> </td> 
  </tr> 
 </tbody> 
</table>

