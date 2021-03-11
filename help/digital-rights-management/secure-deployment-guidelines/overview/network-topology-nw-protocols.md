---
description: Ao configurar uma arquitetura de rede segura, os protocolos de rede são necessários para a interação entre o DRM Adobe Primetime e outros sistemas na rede corporativa.
title: Protocolos de rede Adobe Primetime DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Protocolos de rede Adobe Primetime DRM {#adobe-primetime-drm-network-protocols}

Ao configurar uma arquitetura de rede segura, os protocolos de rede são necessários para a interação entre o DRM Adobe Primetime e outros sistemas na rede corporativa.

Ao configurar uma arquitetura de rede segura, os seguintes protocolos de rede são necessários para essa interação:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocolo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Use </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os clientes Flash Player, Adobe AIR® e Adobe Primetime se comunicam com o Primetime DRM por HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (opcional) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os clientes do Flash Player, Adobe AIR e Adobe Primetime podem usar HTTPS para se comunicar com o DRM do Primetime; HTTPS (SSL) não é necessário a menos que você suporte clientes FMRMS 1.x. Para obter mais informações, consulte <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> URLs de entrada </a> e Configuração do SSL. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Portas para servidores de aplicativos {#ports-for-application-servers}

Você pode configurar o servidor de licenças Adobe Primetime DRM para usar qualquer porta de rede.

Essas portas devem ser ativadas ou desativadas no firewall interno, dependendo da funcionalidade de rede que você deseja permitir para clientes que se conectam ao servidor de aplicativos que executa o Primetime DRM.

## Configurar SSL {#configuring-ssl}

A SSL (Secure Sockets Layer) é necessária apenas se você precisar de suporte para clientes Flash Media Rights Management Server 1.x.

O SSL com autenticação de cliente é necessário para o Adobe Primetime DRM Key Server. Para obter mais informações, consulte [Usando o Adobe Primetime DRM Key Server](../../using-the-drm-key-server/requirements.md).