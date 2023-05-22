---
title: Visão geral da classe DRMStatusEvent
description: Visão geral da classe DRMStatusEvent
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---


# Visão geral {#using-the-drmstatusevent-class-overview}

A `DRMStatusEvent` O objeto é despachado quando o conteúdo protegido pelo Primetime DRM começa a ser reproduzido com sucesso. (O sucesso implica que a licença é verificada e que o usuário é autenticado e autorizado a visualizar o conteúdo).

A variável `DRMStatusEvent` o objeto contém informações relacionadas à licença, incluindo se a licença pode ser disponibilizada offline ou quando a licença expira e o conteúdo não pode mais ser exibido.
