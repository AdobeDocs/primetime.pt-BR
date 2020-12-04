---
description: Os clientes podem usar o DRM de AAXS (Adobe Access) com seus próprios sistemas de gerenciamento de chave de conteúdo (CKMS) com o recurso CEK externo.
seo-description: Os clientes podem usar o DRM de AAXS (Adobe Access) com seus próprios sistemas de gerenciamento de chave de conteúdo (CKMS) com o recurso CEK externo.
seo-title: Visão geral do CEK externo do DRM de acesso ao Adobe
title: Visão geral do CEK externo do DRM de acesso ao Adobe
uuid: ea0bba63-7743-4216-863f-392500998eb6
translation-type: tm+mt
source-git-commit: 92e04cbb5e94f60c8d06e94b826ff9361c10ef97
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Visão geral do CEK externo do DRM de acesso Adobe {#adobe-access-drm-external-cek-overview}

Os clientes podem usar o DRM de AAXS (Adobe Access) com seus próprios sistemas de gerenciamento de chave de conteúdo (CKMS) com o recurso CEK externo.

Por padrão, o DRM de AAXS (Adobe Access) abstrai a necessidade de manipular diretamente as chaves, os certificados e os metadados DRM durante o processo de empacotamento do conteúdo. O AAXS Java SDK gerará automaticamente uma chave de criptografia de conteúdo aleatória (CEK) durante o tempo de empacotamento e a usará para criptografar o conteúdo. Em seguida, o SDK criptografa o CEK em si e o insere nos metadados do conteúdo. No momento da emissão da licença, o servidor AAXS só precisa da chave privada do servidor de licenças AAXS para acessar o CEK a partir dos metadados para gerar uma licença.
