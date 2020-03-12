---
seo-title: Visão geral das preferências de configuração
title: Visão geral das preferências de configuração
uuid: d1c067b1-6c2b-460e-8d00-5a5bfee0789c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Visão geral das preferências de configuração {#setting-preferences-overview}

Com exceção do URL do servidor Packager, todas as preferências especificadas abaixo são armazenadas no [!DNL flashaccess-refimpl-packager.properties] arquivo no servidor. Todas as configurações podem ser modificadas diretamente no arquivo de propriedades ou pelo aplicativo AIR. As senhas são criptografadas quando são armazenadas no arquivo de propriedades no servidor. Digite a senha não criptografada na interface do usuário e ela será criptografada antes de ser armazenada no arquivo.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Todos os diretórios e caminhos se referem aos diretórios no servidor Packager, não ao cliente que está executando o aplicativo AIR.

Quaisquer alterações feitas aqui entrarão em vigor imediatamente depois que as preferências forem salvas. Não há necessidade de reiniciar o servidor, a menos que o Thread do Packager seja encerrado devido a problemas de configuração.

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
   <td colname="1" class="- topic/entry "> URL do servidor Packager </td> 
   <td colname="2" class="- topic/entry "> Localização do servidor que executa <span class="filepath"> flashaccess-packager.war </span>; por exemplo, <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Diretório de recursos </td> 
   <td colname="2" class="- topic/entry "> Diretório que contém políticas, certificados, credenciais e quaisquer outros recursos necessários para o servidor do Packager </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL do servidor de licenças </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL do servidor do qual o cliente deve solicitar uma licença; por exemplo, <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

