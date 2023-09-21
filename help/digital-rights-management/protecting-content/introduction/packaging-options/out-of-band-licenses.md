---
title: Licenças fora de banda
description: Licenças fora de banda
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Licenças fora de banda {#out-of-band-licenses}

Usando o Primetime DRM, você pode implementar um fluxo de trabalho no qual os clientes obtêm licenças pré-geradas fora de banda e, portanto, eliminar a necessidade de implantar um servidor de licenças. Para dar suporte a esse fluxo de trabalho, uma opção indicando que nenhum servidor de licença está disponível deve ser especificada no momento do empacotamento. Isso impede que o cliente tente solicitar uma licença para esse conteúdo de um servidor de licenças.

O conteúdo que indica a indisponibilidade de um servidor de licenças só pode ser reproduzido nos clientes Primetime DRM versão 3.0 ou posterior. Os clientes mais antigos precisam atualizar para reproduzir este conteúdo.
