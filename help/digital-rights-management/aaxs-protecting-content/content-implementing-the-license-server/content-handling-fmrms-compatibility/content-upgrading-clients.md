---
title: Atualização de clientes
description: Atualização de clientes
copied-description: true
exl-id: 0476c9ef-3622-4bc5-bb24-f8543470b7d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Atualização de clientes{#upgrading-clients}

Se um cliente FMRMS 1.x contatar um servidor de acesso Adobe, o servidor precisará solicitar que o cliente atualize.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* O URL da solicitação é &quot;*URL base do conteúdo 1.x*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   Ao contrário de outros manipuladores de solicitação de acesso ao Adobe, esse manipulador não fornece acesso a nenhuma informação de solicitação ou requer que dados de resposta sejam definidos. Crie uma instância do `FMRMSv1RequestHandler`, e chame `close()`
