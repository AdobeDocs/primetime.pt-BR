---
title: Arquivo de propriedades do servidor de licenças
description: Arquivo de propriedades do servidor de licenças
copied-description: true
exl-id: ac105ea6-b5a4-4416-bf17-f619abcf7cd5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Arquivo de propriedades do servidor de licenças {#license-server-properties-file}

Use o [!DNL flashaccess-refimpl.properties] arquivo para configurar o componente License Server da implementação de referência. No mínimo, certifique-se de configurar as propriedades relacionadas à Credencial de transporte e à Credencial do servidor de licenças. Os locais dos arquivos de credencial devem ser especificados em relação ao diretório especificado pelo `config.resourcesDirectory` propriedade. Esse arquivo também contém várias propriedades relacionadas ao conteúdo do empacotamento: essas propriedades são usadas apenas para a conversão de metadados do Flash Media Rights Management Server 1.x. Se você modificar qualquer um dos valores nesse arquivo de propriedades, será necessário reiniciar o servidor de licenças para que as alterações entrem em vigor.

Para dar suporte à geração de licenças para entrega de Chave Remota para clientes iOS no Adobe Access, o certificado do Servidor de Chaves deve ser especificado em [!DNL flashaccess-refimpl.properties].

As seguintes propriedades foram adicionadas no Acesso ao Adobe:

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
   <td colname="2" class="- topic/entry "> Certificado de servidor de licença do servidor de chave, emitido pelo Adobe. Este certificado é usado para gerar licenças para dispositivos iOS, quando os metadados indicam que um servidor de chaves é necessário. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Alias do certificado de servidor de licenças emitido por Adobe do servidor de chaves armazenado no HSM. Quando o HSM estiver ativado, use essa propriedade em vez de <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>
