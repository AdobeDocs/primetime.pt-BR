---
title: Metadados personalizados
description: Metadados personalizados
copied-description: true
exl-id: cfc8b17b-c077-4b28-896d-b1ede1d5090b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Metadados personalizados {#custom-metadata}

Use isso para adicionar pares de chave/valor personalizados aos metadados de conteúdo que podem ser interpretados pelo aplicativo do servidor.

O formato de metadados para o conteúdo DRM do Primetime permite incluir pares de chave/valor personalizados no momento do empacotamento. Esses metadados personalizados podem ser processados pelo servidor de licenças durante a emissão da licença. Os metadados são separados de uma política DRM do Primetime e podem ser exclusivos para cada seção do conteúdo.

Exemplo de caso de uso: durante uma fase Beta, você pode incluir a propriedade personalizada `Release:BETA` no momento da embalagem. Os servidores de licenças podem enviar licenças para esse conteúdo durante o período Beta. No entanto, após a expiração do período Beta, os servidores de licença não permitem acesso ao conteúdo.
