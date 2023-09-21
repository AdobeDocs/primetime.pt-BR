---
title: Visão geral da solicitação de certificados
description: Visão geral da solicitação de certificados
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Visão geral {#request-certificates-overview}

Para usar o SDK de produção do Adobe Primetime DRM, repita as seguintes etapas para solicitar cada certificado (Servidor de licenças, Empacotador e Transporte). O SDK de avaliação e o SDK de avaliação usam um único certificado.

>[!NOTE]
>
>Os exemplos fornecidos neste documento usam OpenSSL. Você também pode usar outros utilitários. Use esses exemplos somente para referência. Para obter informações sobre a geração de pares de chaves e o armazenamento de chaves e certificados no HSM (Hardware Security Module, módulo de segurança de hardware), consulte a documentação do HSM.
