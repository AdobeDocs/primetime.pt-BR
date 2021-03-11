---
title: Visão geral das preferências de configuração
description: Visão geral das preferências de configuração
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Visão geral das preferências de configuração {#setting-preferences-overview}

Com exceção do URL do Servidor do Packager, todas as preferências especificadas abaixo são armazenadas no arquivo [!DNL flashaccess-refimpl-packager.properties] no servidor. Todas as configurações podem ser modificadas diretamente no arquivo de propriedades ou por meio do aplicativo AIR. As senhas são criptografadas quando armazenadas no arquivo de propriedades do servidor. Digite a senha não criptografada na interface do usuário e ela será criptografada antes de ser armazenada no arquivo.

>[!NOTE]
>
>Todos os diretórios e caminhos se referem a diretórios no servidor do empacotador, não no cliente que está executando o aplicativo AIR.

Todas as alterações feitas aqui entrarão em vigor imediatamente após as preferências serem salvas. Não há necessidade de reiniciar o servidor a menos que o Thread do Packager seja encerrado devido a problemas de configuração.

As descrições de preferências usam os seguintes termos:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Preferência </th> 
   <th colname="2" class="- topic/entry entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL do servidor do pacote </td> 
   <td colname="2" class="- topic/entry "> Local do servidor executando <span class="filepath"> flashaccess-packager.war </span>; por exemplo, <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Diretório de recursos </td> 
   <td colname="2" class="- topic/entry "> Diretório contendo políticas, certificados, credenciais e quaisquer outros recursos necessários para o servidor do empacotador </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL do Servidor de Licenças </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL do servidor do qual o cliente deve solicitar uma licença; por exemplo, <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

