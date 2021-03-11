---
title: Servidor de licenças DRM do Primetime
description: Servidor de licenças DRM do Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Servidor de licenças DRM do Primetime {#primetime-drm-license-server}

O servidor de licenças de DRM do Primetime é criado a partir do SDK Java de DRM do Primetime. Este servidor consome solicitações de licença de clientes que solicitam acesso a conteúdo protegido. O servidor tem a capacidade de analisar e manipular a Política de DRM a partir da solicitação de licença, a fim de modificar ou substituir a política antes de usar a política para gerar uma licença para o cliente solicitante.

Para implantar um servidor de licença de DRM Primetime, ele deve primeiro atender **às regras de conformidade e robustez** para DRM Primetime. O Adobe também oferece um serviço de licenciamento de DRM do Primetime hospedado chamado [DRM da Primetime Cloud](../cloud-quick-start/whats-included.md), que pode ser usado como uma alternativa para hospedar seu próprio servidor de licenças.
