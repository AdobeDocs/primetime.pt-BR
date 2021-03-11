---
title: Informações de segurança específicas do fornecedor
description: Informações de segurança específicas do fornecedor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Informações de segurança específicas do fornecedor{#vendor-specific-security-information}

Esta seção contém informações relacionadas à segurança sobre sistemas operacionais e servidores de aplicativos que são incorporados à solução de Acesso ao Adobe.

Use os links fornecidos nesta seção para encontrar informações de segurança específicas do fornecedor para seu sistema operacional e servidor de aplicativos.

## Informações de segurança do sistema operacional {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

Ao proteger seu sistema operacional, implemente cuidadosamente as medidas descritas pelo fornecedor do sistema operacional, incluindo estas:

* Definir e controlar usuários, atribuições e privilégios
* Monitorar logs e trilhas de auditoria
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
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guia de segurança do Windows Server 2008</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5 e 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guia de segurança Red Hat Enterprise Linux 5</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

A tabela a seguir descreve algumas possíveis abordagens para minimizar as vulnerabilidades de segurança encontradas no sistema operacional.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Item </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Correções de segurança </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Há um risco maior de um usuário não autorizado ter acesso ao servidor de aplicativos se os patches e upgrades de segurança do fornecedor não forem aplicados em tempo hábil. Teste os patches de segurança antes de aplicá-los aos servidores de produção. </p> <p class="- topic/p ">Além disso, crie políticas e procedimentos para verificar e instalar patches regularmente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software de proteção antivírus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os scanners de vírus podem identificar arquivos infectados digitalizando uma assinatura ou observando um comportamento incomum. Os scanners mantêm suas assinaturas de vírus em um arquivo, que geralmente é armazenado no disco rígido local. Como os novos vírus são detectados com frequência, é necessário atualizar esse arquivo com frequência para que o mecanismo de varredura de vírus identifique todos os vírus atuais. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Protocolo de Hora da Rede (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para operações adequadas e análises forenses, mantenha o tempo preciso nos servidores de Adobe Access e nos pacotes de Adobe Access. Use uma versão segura do NTP para sincronizar o tempo em todos os sistemas conectados à Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informações de segurança do servidor de aplicativos {#section-EBB4EF371CFF4A848694CC240B23D404}

Ao proteger seu servidor de aplicativos, você deve implementar as medidas descritas pelo fornecedor do servidor, incluindo estas:

* Uso de nome de usuário de administrador não óbvio
* Desativação de serviços desnecessários
* Proteção do gerenciador de console
* Ativação de cookies seguros
* Fechamento de portas desnecessárias
* Limitação de interfaces administrativas por endereços IP ou domínios
* Uso do Gerenciador de segurança Java™

