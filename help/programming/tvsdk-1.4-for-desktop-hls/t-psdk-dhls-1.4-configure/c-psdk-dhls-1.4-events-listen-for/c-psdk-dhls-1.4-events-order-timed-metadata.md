---
description: O TVSDK despacha eventos de metadados cronometrados e gera metadados cronometrados sempre que tags padrão ou personalizadas são encontradas ou quando uma lista de reprodução é alterada em um manifesto. Eventos são despachados na ordem em que aparecem no manifesto.
title: Eventos de metadados cronometrados
exl-id: 4c58b06e-5f70-452c-a743-55c4b6206711
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Eventos de metadados cronometrados{#timed-metadata-events}

O TVSDK despacha eventos de metadados cronometrados e gera metadados cronometrados sempre que tags padrão ou personalizadas são encontradas ou quando uma lista de reprodução é alterada em um manifesto. Eventos são despachados na ordem em que aparecem no manifesto.

Seu reprodutor implementa ações com base nos seguintes eventos:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: despachado quando um metadado de ID3 cronometrado foi processado.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: despachado quando os metadados cronometrados eram processados e nenhuma oportunidade era detectada.
