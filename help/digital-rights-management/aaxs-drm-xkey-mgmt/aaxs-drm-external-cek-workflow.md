---
title: Fluxo de trabalho CEK externo do DRM AXS
description: Esse workflow é uma saída da maioria dos sistemas DRM existentes, pois não requer o uso de nenhum repositório central ou do Sistema de Gerenciamento de Chave de Conteúdo (CKMS)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Fluxo de trabalho CEK externo do DRM AXS{#aaxs-drm-external-cek-workflow}

Esse workflow é uma saída da maioria dos sistemas DRM existentes, pois não requer o uso de nenhum repositório central ou do Sistema de Gerenciamento de Chave de Conteúdo (CKMS). No entanto, para os clientes que desejam que o AXS funcione com seu CKMS existente, o AAXS fornece um recurso chamado &quot;CEK externo&quot;, no qual o CEK é fornecido externamente no momento da embalagem e da emissão da licença.

![](assets/ECEK_Workflow.PNG)

1. (Pacote) O AAXS Java SDK é fornecido com um CEK e uma CEK ID.
1. (Pacote) O CEK é usado para criptografar conteúdo.
1. (Pacote) A ID do CEK é inserida nos metadados DRM do conteúdo.
1. O dispositivo tenta reproduzir o conteúdo solicitando uma licença do servidor AXS.
1. (Licenciamento) O servidor AAXS extrai a ID do CEK dos metadados de conteúdo.
1. O servidor AAXS recupera o CEK do CKMS.
1. (Licenciamento) O servidor AXS emite ao dispositivo uma licença que contém o CEK.
