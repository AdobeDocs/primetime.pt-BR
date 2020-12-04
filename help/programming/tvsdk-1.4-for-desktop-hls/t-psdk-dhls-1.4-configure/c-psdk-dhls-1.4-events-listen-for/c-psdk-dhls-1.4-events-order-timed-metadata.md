---
description: O TVSDK despacha eventos de metadados cronometrados e gera metadados sempre que tags padrão ou personalizadas são encontradas ou quando uma lista de reprodução muda em um manifesto. Os eventos são despachados na ordem em que aparecem no manifesto.
seo-description: O TVSDK despacha eventos de metadados cronometrados e gera metadados sempre que tags padrão ou personalizadas são encontradas ou quando uma lista de reprodução muda em um manifesto. Os eventos são despachados na ordem em que aparecem no manifesto.
seo-title: Eventos de metadados cronometrados
title: Eventos de metadados cronometrados
uuid: 69c43701-6ffa-45fe-a104-fe81391222e7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Eventos de metadados cronometrados{#timed-metadata-events}

O TVSDK despacha eventos de metadados cronometrados e gera metadados sempre que tags padrão ou personalizadas são encontradas ou quando uma lista de reprodução muda em um manifesto. Os eventos são despachados na ordem em que aparecem no manifesto.

Seu player implementa ações com base nos seguintes eventos:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Despachado quando metadados cronometrados ID3 eram processados.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Despachado quando os metadados cronometrados eram processados e nenhuma oportunidade era detectada.

