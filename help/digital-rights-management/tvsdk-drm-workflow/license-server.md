---
title: Servidor de licença de DRM do Primetime
description: Servidor de licença de DRM do Primetime
copied-description: true
exl-id: 2927bb21-0001-46d4-aae1-a277f414560d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Servidor de licença de DRM do Primetime {#primetime-drm-license-server}

O servidor de licença do Primetime DRM é criado a partir do SDK do Java do Primetime DRM. Esse servidor consome solicitações de licença de clientes que solicitam acesso ao conteúdo protegido. O servidor pode analisar e manipular a Política DRM de dentro da solicitação de licença para modificar ou substituir a política antes de usá-la para gerar uma licença para o cliente solicitante.

Para implantar um servidor de licença de DRM do Primetime, ele deve primeiro atender **Regras de conformidade e robustez do Adobe** para o Primetime DRM. O Adobe também oferece um serviço de licenciamento DRM do Primetime hospedado, chamado [DRM do Primetime Cloud](../cloud-quick-start/whats-included.md), que você pode usar como uma alternativa para hospedar seu próprio servidor de licenças.
