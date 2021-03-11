---
title: Arquivo de propriedades do servidor de licenças
description: Arquivo de propriedades do servidor de licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Arquivo de propriedades do servidor de licenças {#license-server-properties-file}

Use o arquivo [!DNL flashaccess-refimpl.properties] para configurar o componente do License Server da implementação de referência. No mínimo, certifique-se de configurar as propriedades relacionadas à Credencial de Transporte e à Credencial do Servidor de Licenças. Os locais dos arquivos de credencial devem ser especificados em relação ao diretório especificado pela propriedade `config.resourcesDirectory`. Esse arquivo também contém várias propriedades relacionadas ao conteúdo do empacotamento: essas propriedades são usadas apenas para conversão de metadados do Flash Media Rights Management Server 1.x. Se modificar qualquer um dos valores neste arquivo de propriedade, será necessário reiniciar o servidor de licenças para que as alterações entrem em vigor.

Para suportar a geração de licenças para entrega de Chave Remota a clientes iOS no Adobe Access, o certificado do Servidor de Chave deve ser especificado em [!DNL flashaccess-refimpl.properties].

As seguintes propriedades foram adicionadas ao Adobe Access:

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
   <td colname="2" class="- topic/entry "> Certificado do Servidor de Licenças do Servidor de Chave, emitido pelo Adobe. Esse certificado é usado para gerar licenças para dispositivos iOS, quando os metadados indicam que um Servidor de chaves é necessário. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Alias do certificado do Servidor de Licenças emitido por Adobe do Servidor de Chave armazenado no HSM. Quando o HSM estiver ativado, use essa propriedade em vez de <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>

