---
title: Pré-requisitos
description: Pré-requisitos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Pré-requisitos {#prerequisites}

Antes de empacotar o conteúdo, é necessário um certificado do Empacotador de DRM do Primetime. Ela deve ser solicitada por meio do Processo de Registro de Certificado DRM do Primetime. Somente um certificado de empacotador é necessário (sem License Server ou Transporte). Indique no e-mail de solicitação de certificado que a solicitação é para um certificado a ser usado com o serviço DRM.

[Guia de Registro de Certificado](../../digital-rights-management/certificate-enrollment-guide/about-certs.md)

Há dois níveis de certificados de empacotamento - PRODUÇÃO e AVALIAÇÃO. O conteúdo que é empacotado usando certificados de AVALIAÇÃO é somente para uso de desenvolvimento e não será reproduzido após a expiração do certificado. Todas as licenças emitidas para conteúdo de AVALIAÇÃO terão uma data de expiração máxima da política embutida em código igual à data de expiração do certificado (se não estiver definida na política DRM).
