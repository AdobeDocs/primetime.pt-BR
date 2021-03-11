---
title: Visão geral dos certificados de solicitação
description: Visão geral dos certificados de solicitação
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Visão geral {#request-certificates-overview}

Para usar o SDK de produção de DRM da Adobe Primetime, repita as etapas a seguir para solicitar cada certificado (License Server, Packager e Transport). O SDK de avaliação e o SDK de avaliação usam um único certificado.

>[!NOTE]
>
>Os exemplos fornecidos neste documento usam OpenSSL. Você também pode usar outros utilitários. Use estes exemplos somente para referência. Para obter informações sobre a geração de pares de chaves e o armazenamento de chaves e certificados em seu Módulo de segurança de hardware (HSM), consulte a documentação do seu HSM.