---
description: Você pode substituir o comportamento padrão de como o TVSDK procura por anúncios ao usar marcadores de anúncios personalizados.
seo-description: Você pode substituir o comportamento padrão de como o TVSDK procura por anúncios ao usar marcadores de anúncios personalizados.
seo-title: Controle o comportamento de reprodução para busca em marcadores de anúncio personalizados
title: Controle o comportamento de reprodução para busca em marcadores de anúncio personalizados
uuid: 926299c6-9c23-457d-b836-08432e4e169e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Controle o comportamento de reprodução para busca em marcadores de anúncio personalizados{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Você pode substituir o comportamento padrão de como o TVSDK procura por anúncios ao usar marcadores de anúncios personalizados.

Por padrão, quando um usuário busca por seções de anúncios passadas ou para dentro que resultam do posicionamento de marcadores de anúncios personalizados, o TVSDK ignora os anúncios. Isso pode ser diferente do comportamento atual de reprodução para quebras de anúncios padrão.

Você pode pedir ao TVSDK para reposicionar o indicador de reprodução no início do anúncio personalizado ignorado mais recentemente quando o usuário buscar mais de um ou mais anúncios personalizados.

1. Configure uma instância de Metadados com a enumeração `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` definida com o valor da string &quot;true&quot; (não como um Booliano `true`).

1. Crie e configure uma `MediaResource` instância, transmitindo as opções de configuração adicionais para `TimeRangeCollection.toMetadata`. Este método recebe opções de configuração adicionais por meio de outra estrutura de metadados genérica.

