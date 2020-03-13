---
seo-title: Fluxo de trabalho CEK externo do DRM AAXS
title: Fluxo de trabalho CEK externo do DRM AAXS
description: Esse fluxo de trabalho é uma saída da maioria dos sistemas DRM existentes, pois não requer o uso de nenhum repositório central ou do Content Key Management System (CKMS)
seo-description: Esse fluxo de trabalho é uma saída da maioria dos sistemas DRM existentes, pois não requer o uso de nenhum repositório central ou do Content Key Management System (CKMS)
uuid: b313594b-0feb-4f27-bf02-f04b955e2140
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc

---


# Fluxo de trabalho CEK externo do DRM AAXS{#aaxs-drm-external-cek-workflow}

Esse fluxo de trabalho é uma saída da maioria dos sistemas DRM existentes, pois não requer o uso de nenhum repositório central ou do Content Key Management System (CKMS). No entanto, para os clientes que desejam que o AXS trabalhe com seus CKMS existentes, o AAXS fornece um recurso chamado &quot;CEK externo&quot;, no qual o CEK é fornecido externamente no momento da embalagem e da emissão da licença.

![](assets/ECEK_Workflow.PNG)

1. (Pacote) O AAXS Java SDK é fornecido com uma CEK e uma CEK ID.
1. (Pacote) O CEK é usado para criptografar conteúdo.
1. (Pacote) A ID CEK é inserida nos metadados DRM do conteúdo.
1. O dispositivo tenta reproduzir conteúdo solicitando uma licença do servidor AAXS.
1. (Licenciamento) O servidor AXS extrai a ID CEK dos metadados do conteúdo.
1. O servidor AAXS recupera o CEK do CKMS.
1. (Licenciamento) O servidor AAXS emite ao dispositivo uma licença que contém o CEK.
