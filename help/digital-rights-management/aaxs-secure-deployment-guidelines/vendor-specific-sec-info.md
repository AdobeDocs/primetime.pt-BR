---
title: Informações de segurança específicas do fornecedor
description: Informações de segurança específicas do fornecedor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Informações de segurança específicas do fornecedor{#vendor-specific-security-information}

Esta seção contém informações relacionadas à segurança dos sistemas operacionais e servidores de aplicativos que estão incorporados à sua solução de acesso ao Adobe.

Use os links fornecidos nesta seção para encontrar informações de segurança específicas do fornecedor para seu sistema operacional e servidor de aplicativos.

## Informações de segurança do sistema operacional {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

Ao proteger seu sistema operacional, implemente cuidadosamente as medidas descritas pelo fornecedor do sistema operacional, incluindo estas:

* Definindo e controlando usuários, atribuições e privilégios
* Monitorar logs e trilhas de auditoria
* Remoção de serviços e aplicativos desnecessários
* Fazendo backup de arquivos

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
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008, edição Enterprise ou Standard </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guia de segurança do Windows Server 2008</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5 e 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guia de segurança do Red Hat Enterprise Linux 5</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

A tabela a seguir descreve algumas abordagens possíveis para minimizar as vulnerabilidades de segurança encontradas no sistema operacional.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Há um risco maior de que um usuário não autorizado possa obter acesso ao servidor de aplicativos se os patches e as atualizações de segurança do fornecedor não forem aplicados em tempo hábil. Teste os patches de segurança antes de aplicá-los aos servidores de produção. </p> <p class="- topic/p ">Além disso, crie políticas e procedimentos para verificar e instalar patches regularmente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software de proteção contra vírus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Verificadores de vírus podem identificar arquivos infectados ao verificar uma assinatura ou observar comportamento incomum. Os scanners mantêm suas assinaturas de vírus em um arquivo, que geralmente é armazenado no disco rígido local. Como novos vírus são descobertos com frequência, você deve atualizar esse arquivo com frequência para que o verificador de vírus identifique todos os vírus atuais. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Protocolo de tempo de rede (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para a operação adequada e análise jurídica, mantenha o tempo preciso nos servidores de Acesso ao Adobe e nos Packagers de Acesso ao Adobe. Use uma versão segura de NTP para sincronizar o horário em todos os sistemas conectados à Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informações de segurança do servidor de aplicativos {#section-EBB4EF371CFF4A848694CC240B23D404}

Ao proteger o servidor de aplicativos, você deve implementar as medidas descritas pelo fornecedor do servidor, incluindo estas:

* Uso de nome de usuário de administrador não óbvio
* Desabilitar serviços desnecessários
* Proteção do gerenciador de console
* Ativação de cookies seguros
* Fechando portas desnecessárias
* Limitação de interfaces administrativas por endereços IP ou domínios
* Utilização do Gerenciador de segurança Java™
