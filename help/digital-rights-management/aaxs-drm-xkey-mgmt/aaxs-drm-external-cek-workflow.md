---
title: Fluxo de Trabalho Externo CEK do AXS DRM
description: Esse fluxo de trabalho é um desvio da maioria dos sistemas DRM existentes, pois não requer o uso de nenhum repositório central ou CKMS (Content Key Management System, sistema de gerenciamento de chaves de conteúdo)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Fluxo de Trabalho Externo CEK do AXS DRM{#aaxs-drm-external-cek-workflow}

Esse fluxo de trabalho é um desvio da maioria dos sistemas DRM existentes, pois não requer o uso de nenhum repositório central ou Sistema de gerenciamento de chaves de conteúdo (CKMS). No entanto, para clientes que desejam que o AXS funcione com seu CKMS existente, o AXS fornece um recurso chamado &quot;CEK externo&quot;, no qual o CEK é fornecido externamente no momento da emissão da embalagem e da licença.

![](assets/ECEK_Workflow.PNG)

1. (Pacote) O SDK Java AXS é fornecido com um CEK e uma ID de CEK.
1. (Pacote) O CEK é usado para criptografar o conteúdo.
1. (Pacote) A ID do CEK é inserida nos metadados DRM do conteúdo.
1. O dispositivo tenta reproduzir o conteúdo solicitando uma licença ao servidor AXS.
1. (Licenciamento) O servidor AXS extrai a ID do CEK dos metadados de conteúdo.
1. O servidor AXS recupera o CEK do CKMS.
1. (Licenciamento) O servidor AXS emite para o dispositivo uma licença que contém o CEK.
