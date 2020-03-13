---
seo-title: Metadados personalizados
title: Metadados personalizados
uuid: 99bdef62-32a9-4fd0-919c-5a2594e8d17e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Metadados personalizados {#custom-metadata}

Use essa opção para adicionar pares de chave/valor personalizados aos metadados de conteúdo que podem ser interpretados pelo aplicativo do servidor.

O formato de metadados do conteúdo DRM do Primetime permite que você inclua pares de chave/valor personalizados no momento do empacotamento. Esses metadados personalizados podem ser processados pelo servidor de licenças durante a emissão de licenças. Os metadados são separados de uma política DRM Primetime e podem ser exclusivos para cada seção do conteúdo.

Exemplo de caso de uso: Durante uma fase Beta, é possível incluir a propriedade personalizada `Release:BETA` no momento do empacotamento. Os servidores de licença podem enviar licenças para este conteúdo durante o período Beta. No entanto, após o período Beta expirar, os servidores de licença não permitem acesso ao conteúdo.
