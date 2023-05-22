---
description: Os clientes podem usar o DRM de Acesso ao Adobe (AXS) com seus próprios CKMS (Content Key Management Systems, sistemas de gerenciamento de chaves de conteúdo) com o recurso CEK externo.
title: Visão geral do CEK externo de DRM de acesso ao Adobe
exl-id: 4131863b-5773-4222-aae9-d984267cdb86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Visão geral do CEK externo de DRM de acesso ao Adobe {#adobe-access-drm-external-cek-overview}

Os clientes podem usar o DRM de Acesso ao Adobe (AXS) com seus próprios CKMS (Content Key Management Systems, sistemas de gerenciamento de chaves de conteúdo) com o recurso CEK externo.

Por padrão, o DRM de Adobe (AXS) abstrai a necessidade de manipular diretamente chaves, certificados e metadados de DRM durante o processo de empacotamento de conteúdo. O AXS Java SDK gerará automaticamente uma Chave de criptografia de conteúdo (CEK) aleatória durante o tempo de empacotamento e a usará para criptografar o conteúdo. Em seguida, o SDK criptografa o próprio CEK e o insere nos metadados do conteúdo. No momento da emissão da licença, o servidor AXS só precisa de sua chave privada do servidor de licenças AXS para acessar o CEK a partir dos metadados para gerar uma licença.
