---
seo-title: Atualizando clientes
title: Atualizando clientes
uuid: 9c9bc7da-2a97-4659-945a-554d778d30a3
translation-type: tm+mt
source-git-commit: 5cf90a75d8805fb64d7d145722ad10a1ce77a14d
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Atualizando clientes{#upgrading-clients}

Se um cliente FMRMS 1.x entrar em contato com um servidor de acesso a Adobe, o servidor precisará solicitar que o cliente atualize.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* O URL da solicitação é &quot;*URL base de conteúdo 1.x*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   Ao contrário de outros manipuladores de solicitação de acesso a Adobe, esse manipulador não fornece acesso a nenhuma informação de solicitação ou requer que qualquer dado de resposta seja definido. Crie uma instância de `FMRMSv1RequestHandler` e chame `close()`