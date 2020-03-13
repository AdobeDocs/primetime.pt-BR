---
seo-title: Informações de segurança específicas do fornecedor
title: Informações de segurança específicas do fornecedor
uuid: 23186770-c73a-4802-bc30-fa9e4b47d9ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Informações de segurança específicas do fornecedor{#vendor-specific-security-information}

Esta seção contém informações relacionadas à segurança sobre sistemas operacionais e servidores de aplicativos que estão incorporados à sua solução Adobe Access.

Use os links fornecidos nesta seção para encontrar informações de segurança específicas do fornecedor para seu sistema operacional e servidor de aplicativos.

## Informações de segurança do sistema operacional {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

Ao proteger seu sistema operacional, implemente cuidadosamente as medidas descritas pelo fornecedor do sistema operacional, incluindo estas:

* Definição e controle de usuários, funções e privilégios
* Registros de monitoramento e trilhas de auditoria
* Remoção de serviços e aplicativos desnecessários
* Backup de arquivos

Para obter informações de segurança sobre sistemas operacionais compatíveis com o Adobe Access, consulte os recursos nesta tabela.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Sistema operacional </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Recurso de segurança </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008 Enterprise ou Standard Edition </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guia de Segurança do Windows Server 2008</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5 e 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guia de segurança Red Hat Enterprise Linux 5</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

A tabela a seguir descreve algumas abordagens possíveis para minimizar vulnerabilidades de segurança que são encontradas no sistema operacional.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Item </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Patches de segurança </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Existe um risco aumentado de que um usuário não autorizado possa obter acesso ao servidor de aplicativos se os patches e atualizações de segurança do fornecedor não forem aplicados em tempo hábil. Teste os patches de segurança antes de aplicá-los aos servidores de produção. </p> <p class="- topic/p ">Além disso, crie políticas e procedimentos para verificar e instalar patches regularmente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software de proteção contra vírus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os verificadores de vírus podem identificar arquivos infectados digitalizando uma assinatura ou observando um comportamento incomum. Os scanners mantêm suas assinaturas de vírus em um arquivo, que geralmente é armazenado no disco rígido local. Como os novos vírus são descobertos com frequência, você deve atualizar esse arquivo com frequência para que o verificador de vírus identifique todos os vírus atuais. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">NTP (Network Time Protocol, protocolo de tempo de rede) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para operações corretas e análises forenses, mantenha o tempo preciso nos servidores do Adobe Access e nos empacotadores do Adobe Access. Use uma versão segura do NTP para sincronizar o horário em todos os sistemas conectados à Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informações de segurança do servidor de aplicativos {#section-EBB4EF371CFF4A848694CC240B23D404}

Ao proteger o servidor de aplicativos, você deve implementar as medidas descritas pelo fornecedor do servidor, incluindo estas:

* Uso de nome de usuário de administrador não óbvio
* Desativação de serviços desnecessários
* Proteção do gerenciador de console
* Ativação de cookies seguros
* Fechando portas desnecessárias
* Limitação de interfaces administrativas por endereços IP ou domínios
* Uso do Java™ Security Manager

