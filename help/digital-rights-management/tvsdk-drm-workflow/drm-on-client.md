---
title: DRM do Primetime no cliente
description: DRM do Primetime no cliente
copied-description: true
exl-id: 157d558f-3014-4d05-bba1-e73134cedc23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# DRM do Primetime no cliente{#primetime-drm-on-the-client}

Um aplicativo TVSDK do Primetime que reproduz conteúdo protegido deve primeiro chamar as APIs DRM do Primetime para iniciar o fluxo de trabalho para consumo de licença e reprodução de conteúdo protegido. Nesse fluxo de trabalho, o Primetime DRM no cliente cria uma solicitação de licença a partir dos metadados do conteúdo protegido e, em seguida, a envia para o servidor de licença do Primetime DRM.

Antes de emitir a solicitação de licença, o cliente pode, opcionalmente, executar a autenticação/autorização necessária (dependendo de suas regras de negócios).
