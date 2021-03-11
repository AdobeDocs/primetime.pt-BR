---
description: O TVSDK despacha eventos de metadados cronometrados e gera metadados cronometrados sempre que tags padrão ou personalizadas são encontradas ou quando uma lista de reprodução é alterada em um manifesto. Os eventos são despachados na ordem em que aparecem no manifesto.
title: Eventos de metadados cronometrados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Eventos de metadados cronometrados{#timed-metadata-events}

O TVSDK despacha eventos de metadados cronometrados e gera metadados cronometrados sempre que tags padrão ou personalizadas são encontradas ou quando uma lista de reprodução é alterada em um manifesto. Os eventos são despachados na ordem em que aparecem no manifesto.

O reprodutor implementa ações com base nos seguintes eventos:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Despachado quando metadados cronometrados de ID3 eram processados.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Despachado quando os metadados cronometrados eram processados e nenhuma oportunidade era detectada.

