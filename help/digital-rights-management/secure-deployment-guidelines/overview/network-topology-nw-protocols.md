---
description: Quando você configura uma arquitetura de rede segura, são necessários protocolos de rede para a interação entre o Adobe Primetime DRM e outros sistemas em sua rede corporativa.
seo-description: Quando você configura uma arquitetura de rede segura, são necessários protocolos de rede para a interação entre o Adobe Primetime DRM e outros sistemas em sua rede corporativa.
seo-title: Protocolos de rede DRM do Adobe Primetime
title: Protocolos de rede DRM do Adobe Primetime
uuid: 8954e33c-83ac-4b40-9e45-005d4954b44e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Protocolos de rede DRM do Adobe Primetime {#adobe-primetime-drm-network-protocols}

Quando você configura uma arquitetura de rede segura, são necessários protocolos de rede para a interação entre o Adobe Primetime DRM e outros sistemas em sua rede corporativa.

Quando você configura uma arquitetura de rede segura, os seguintes protocolos de rede são necessários para essa interação:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os clientes Flash Player, Adobe AIR e Adobe Primetime podem usar HTTPS para se comunicar com o Primetime DRM; HTTPS (SSL) não é necessário a menos que você suporte clientes FMRMS 1.x. Para obter mais informações, consulte <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> URLs de entrada </a> e Configuração de SSL. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Portas para servidores de aplicativos {#ports-for-application-servers}

Você pode configurar o servidor de licenças DRM do Adobe Primetime para usar qualquer porta de rede.

Essas portas devem ser ativadas ou desativadas no firewall interno, dependendo da funcionalidade de rede que você deseja permitir para clientes que se conectam ao servidor de aplicativos que executa o Primetime DRM.

## Configuração do SSL {#configuring-ssl}

A Secure Sockets Layer (SSL) é necessária somente se você precisar de suporte para clientes do Flash Media Rights Management Server 1.x.

O SSL com autenticação de cliente é necessário para o Adobe Primetime DRM Key Server. Para obter mais informações, consulte [Uso do Adobe Primetime DRM Key Server](../../using-the-drm-key-server/requirements.md).