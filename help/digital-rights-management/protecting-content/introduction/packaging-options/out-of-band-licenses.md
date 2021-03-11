---
title: Licenças fora de banda
description: Licenças fora de banda
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Licenças fora de banda {#out-of-band-licenses}

Usando o DRM do Primetime, você pode implementar um fluxo de trabalho no qual os clientes obtêm licenças pré-geradas fora da banda e, portanto, eliminar a necessidade de implantar um servidor de licenças. Para dar suporte a esse workflow, uma opção indicando que nenhum servidor de licença está disponível deve ser especificada no momento do empacotamento. Isso evita que o cliente tente solicitar uma licença para esse conteúdo de um servidor de licenças.

O conteúdo que indica a indisponibilidade de um servidor de licença só pode ser reproduzido nos clientes DRM do Primetime versão 3.0 ou posterior. Clientes mais antigos precisam atualizar para reproduzir este conteúdo.
