---
description: Os clientes podem usar o DRM do Adobe Access (AXS) com seus próprios sistemas de gerenciamento de chaves de conteúdo (CKMS) com o recurso CEK externo.
title: Visão geral do CEK externo do DRM de acesso a Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Visão geral do CEK externo do DRM de Adobe Access {#adobe-access-drm-external-cek-overview}

Os clientes podem usar o DRM do Adobe Access (AXS) com seus próprios sistemas de gerenciamento de chaves de conteúdo (CKMS) com o recurso CEK externo.

Por padrão, o DRM de Acesso a Adobe (AXS), abstrai a necessidade de manipular diretamente chaves, certificados e metadados de DRM durante o processo de empacotamento de conteúdo. O AAXS Java SDK gerará automaticamente uma Chave de criptografia de conteúdo (CEK) aleatória durante o tempo de empacotamento e a usará para criptografar o conteúdo. Em seguida, o SDK criptografa o CEK propriamente dito e o insere nos metadados do conteúdo. No momento da emissão da licença, o servidor AXS precisa apenas da chave privada do servidor de licenças AXS para acessar o CEK dos metadados para gerar uma licença.
