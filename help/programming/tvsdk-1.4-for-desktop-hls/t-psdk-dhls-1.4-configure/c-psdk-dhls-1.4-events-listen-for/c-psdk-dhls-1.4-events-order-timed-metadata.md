---
description: O TVSDK despacha eventos de metadados cronometrados e gera metadados cronometrados sempre que tags padrão ou personalizadas são encontradas ou quando uma lista de reprodução é alterada em um manifesto. Eventos são despachados na ordem em que aparecem no manifesto.
title: Eventos de metadados cronometrados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Eventos de metadados cronometrados{#timed-metadata-events}

O TVSDK despacha eventos de metadados cronometrados e gera metadados cronometrados sempre que tags padrão ou personalizadas são encontradas ou quando uma lista de reprodução é alterada em um manifesto. Eventos são despachados na ordem em que aparecem no manifesto.

Seu reprodutor implementa ações com base nos seguintes eventos:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: despachado quando um metadado de ID3 cronometrado foi processado.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: despachado quando os metadados cronometrados eram processados e nenhuma oportunidade era detectada.
