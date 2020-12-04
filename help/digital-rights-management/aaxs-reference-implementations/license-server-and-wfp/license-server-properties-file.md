---
seo-title: Arquivo de propriedades do servidor de licenças
title: Arquivo de propriedades do servidor de licenças
uuid: bede307a-2060-451f-baf5-d058702c0a7e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Arquivo de propriedades do servidor de licenças {#license-server-properties-file}

Use o arquivo [!DNL flashaccess-refimpl.properties] para configurar o componente do License Server da implementação de referência. No mínimo, certifique-se de configurar as propriedades relacionadas à Credencial de Transporte e à Credencial do License Server. Os locais dos arquivos de credenciais devem ser especificados em relação ao diretório especificado pela propriedade `config.resourcesDirectory`. Esse arquivo também contém várias propriedades relacionadas ao conteúdo do empacotamento: essas propriedades são usadas apenas para a conversão de metadados 1.x do Flash Media Rights Management Server. Se você modificar qualquer um dos valores neste arquivo de propriedade, será necessário reiniciar o servidor de licenças para que as alterações entrem em vigor.

Para suportar a geração de licenças para o delivery de chave remota para clientes iOS no Adobe Access, o certificado do servidor de chave deve ser especificado em [!DNL flashaccess-refimpl.properties].

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
   <td colname="2" class="- topic/entry "> Certificado do servidor de licença do servidor de chave, emitido pelo Adobe. Este certificado é usado para gerar licenças para dispositivos iOS, quando os metadados indicam que um Servidor-chave é necessário. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Alias do certificado do Servidor de Licenças emitido por Adobe do Servidor de Chaves armazenado no HSM. Quando o HSM estiver ativado, use essa propriedade em vez de <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>

