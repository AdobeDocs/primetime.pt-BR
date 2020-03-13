---
description: Os sistemas operacionais e os servidores de aplicativos estão incluídos na solução Adobe Primetime DRM.
seo-description: Os sistemas operacionais e os servidores de aplicativos estão incluídos na solução Adobe Primetime DRM.
seo-title: Informações de segurança específicas do fornecedor
title: Informações de segurança específicas do fornecedor
uuid: 331baa42-5e19-40a5-bc74-0b1a2cb9370e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Informações de segurança específicas do fornecedor{#vendor-specific-security-information}

Os sistemas operacionais e os servidores de aplicativos estão incluídos na solução Adobe Primetime DRM.

Para encontrar informações de segurança específicas do fornecedor para seu sistema operacional e servidor de aplicativos, consulte Uso do servidor de chaves DRM do Adobe Primetime.

## Informações de segurança do sistema operacional {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

Ao proteger seu sistema operacional, você deve implementar as medidas descritas pelo fornecedor do sistema operacional.

Estas são algumas das medidas:

* Definição e controle de usuários, funções e privilégios
* Registros de monitoramento e trilhas de auditoria
* Remoção de serviços e aplicativos desnecessários
* Backup de arquivos

Estas são algumas informações sobre os sistemas operacionais compatíveis com o Adobe Primetime DRM:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
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

Estas são algumas informações sobre abordagens para minimizar vulnerabilidades de segurança no sistema operacional:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Item </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Patches de segurança </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Existe um risco aumentado de que um usuário não autorizado possa obter acesso ao servidor de aplicativos se os patches e atualizações de segurança do fornecedor não forem aplicados em tempo hábil. </p> <p>Observação:  Certifique-se de testar as correções de segurança antes de aplicá-las aos servidores de produção. </p> <p class="- topic/p ">Você deve criar políticas e procedimentos para verificar e instalar patches regularmente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software de proteção contra vírus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os verificadores de vírus podem identificar arquivos infectados, verificando se há uma assinatura ou comportamento incomum. </p> <p>Os scanners mantêm suas assinaturas de vírus em um arquivo, que geralmente é armazenado no disco rígido local. Novos vírus são detectados com frequência, portanto, é necessário garantir que esse arquivo seja atualizado regularmente. Dessa forma, os verificadores de vírus sempre podem identificar todos os vírus atuais. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">NTP (Network Time Protocol, protocolo de tempo de rede) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Para uma operação correta e análise forense, mantenha o tempo preciso em servidores e empacotadores Primetime DRM. Use uma versão segura do NTP para sincronizar o tempo do Primetime DRM em todos os sistemas conectados à Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informações de segurança do servidor de aplicativos {#section_22986936F1A547CEAB2D97E9E9D4825C}

Ao proteger o servidor de aplicativos, você deve implementar as medidas descritas pelo fornecedor do servidor.

Estas são algumas das medidas a seguir:

* Uso de nome de usuário de administrador não óbvio
* Desativação de serviços desnecessários
* Proteção do gerenciador de console
* Ativação de cookies seguros
* Fechando portas desnecessárias
* Limitação de interfaces administrativas por endereços IP ou domínios
* Uso do Java™ Security Manager

