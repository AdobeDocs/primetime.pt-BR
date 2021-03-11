---
title: Atualizar clientes
description: Atualizar clientes
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Atualizando clientes{#upgrading-clients}

Se um cliente FMRMS 1.x entrar em contato com um servidor de acesso Adobe, o servidor precisará solicitar que o cliente atualize.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* O URL da solicitação é &quot;*URL base do conteúdo 1.x*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   Ao contrário de outros manipuladores de solicitação de acesso ao Adobe, esse manipulador não fornece acesso a informações de solicitação ou requer a definição de dados de resposta. Crie uma instância do `FMRMSv1RequestHandler` e chame `close()`