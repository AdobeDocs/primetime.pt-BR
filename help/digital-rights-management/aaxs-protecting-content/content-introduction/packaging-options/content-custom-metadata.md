---
title: Metadados personalizados
description: Metadados personalizados
copied-description: true
exl-id: d7783420-b345-44de-8f22-a16dda5d7554
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Metadados personalizados {#custom-metadata}

**Especifique a chave/valor personalizado para adicionar aos metadados de conteúdo que podem ser interpretados pelo aplicativo do servidor.**

O formato de metadados de conteúdo de Acesso ao Adobe permite a inclusão de pares de chave/valor personalizados no momento do empacotamento a serem processados pelo servidor de licenças durante a emissão da licença. Esses metadados são separados da política e podem ser exclusivos para cada parte do conteúdo.

Exemplo de caso de uso: durante uma fase Beta, você inclui a propriedade personalizada &quot;Release:BETA&quot; no momento da embalagem. Os servidores de licença podem fornecer licenças para esse conteúdo durante o período Beta, mas após o período Beta expirar, os servidores de licença não permitirão acesso ao conteúdo.
