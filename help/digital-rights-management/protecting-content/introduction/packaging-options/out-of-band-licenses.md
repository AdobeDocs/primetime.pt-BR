---
seo-title: Licenças fora de banda
title: Licenças fora de banda
uuid: 43397ce5-6c52-429d-b7fa-fa8c91cf9742
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Licenças fora de banda {#out-of-band-licenses}

Usando o Primetime DRM, você pode implementar um fluxo de trabalho no qual os clientes obtêm licenças pré-geradas fora da banda e, portanto, eliminar a necessidade de implantar um servidor de licenças. Para suportar esse fluxo de trabalho, uma opção que indica que nenhum servidor de licença está disponível deve ser especificada no momento do empacotamento. Isso impede que o cliente tente solicitar uma licença para esse conteúdo de um servidor de licença.

O conteúdo que indica a indisponibilidade de um servidor de licença só pode ser reproduzido nos clientes Primetime DRM versão 3.0 ou posterior. Clientes mais antigos precisam atualizar para reproduzir este conteúdo.
