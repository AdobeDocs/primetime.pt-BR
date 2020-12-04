---
seo-title: DRM Primetime no cliente
title: DRM Primetime no cliente
uuid: 472180ad-6596-4a24-aa51-7909a75a5e10
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# DRM Primetime no cliente{#primetime-drm-on-the-client}

Um aplicativo Primetime TVSDK que reproduz conteúdo protegido deve primeiro chamar as APIs Primetime DRM para iniciar o fluxo de trabalho de consumo de licença e reprodução de conteúdo protegido. Neste fluxo de trabalho, o Primetime DRM no cliente constrói uma solicitação de licença a partir dos metadados do conteúdo protegido e, em seguida, a envia para o servidor de licenças Primetime DRM.

Antes de emitir a solicitação de licença, o cliente pode, opcionalmente, executar a autenticação/autorização necessária (dependendo das regras de seus negócios).
