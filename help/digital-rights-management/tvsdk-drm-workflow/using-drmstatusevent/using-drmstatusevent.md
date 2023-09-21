---
title: Visão geral da classe DRMStatusEvent
description: Visão geral da classe DRMStatusEvent
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Visão geral da classe DRMStatusEvent {#using-the-drmstatusevent-class-overview}

A `DRMStatusEvent` O objeto é despachado quando o conteúdo protegido pelo Primetime DRM começa a ser reproduzido com sucesso. (O sucesso implica que a licença é verificada e que o usuário é autenticado e autorizado a visualizar o conteúdo).

A variável `DRMStatusEvent` o objeto contém informações relacionadas à licença, incluindo se a licença pode ser disponibilizada offline ou quando a licença expira e o conteúdo não pode mais ser exibido.
