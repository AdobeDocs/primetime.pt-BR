---
title: Metadados personalizados
description: Metadados personalizados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# Metadados personalizados {#custom-metadata}

Use para adicionar pares de chave/valor personalizados aos metadados de conteúdo que podem ser interpretados pelo aplicativo do servidor.

O formato de metadados para o conteúdo DRM do Primetime permite incluir pares de chave/valor personalizados no momento do empacotamento. Esses metadados personalizados podem ser processados pelo servidor de licenças durante a emissão da licença. Os metadados são separados de uma política de DRM do Primetime e podem ser exclusivos para cada seção de conteúdo.

Exemplo de caso de uso: Durante uma fase Beta, você pode incluir a propriedade personalizada `Release:BETA` no momento do empacotamento. Os servidores de licença podem enviar licenças para esse conteúdo durante o período Beta. No entanto, após o período Beta expirar, os servidores de licença não permitirão acesso ao conteúdo.
