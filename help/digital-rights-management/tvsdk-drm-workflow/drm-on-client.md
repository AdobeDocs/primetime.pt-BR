---
title: DRM do Primetime no cliente
description: DRM do Primetime no cliente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# DRM do Primetime no cliente{#primetime-drm-on-the-client}

Um aplicativo Primetime TVSDK que reproduz conteúdo protegido deve chamar primeiro as APIs DRM do Primetime para iniciar o fluxo de trabalho para consumo de licença e reprodução de conteúdo protegido. Nesse fluxo de trabalho, o DRM do Primetime no cliente constrói uma solicitação de licença a partir dos metadados do conteúdo protegido e a envia para o servidor de licença do DRM do Primetime.

Antes de emitir a solicitação de licença, o cliente pode, opcionalmente, executar a autenticação/autorização necessária (dependendo das regras da sua empresa).
