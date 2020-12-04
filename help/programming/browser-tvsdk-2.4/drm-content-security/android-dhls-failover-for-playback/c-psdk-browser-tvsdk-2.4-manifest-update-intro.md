---
description: O TVSDK do navegador pode detectar informações alteradas de reprodução em manifestos principais do m3u8 para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK do navegador suporta um conjunto dinâmico de perfis de taxa de bits à medida que os perfis são exibidos ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre atualizações.
seo-description: O TVSDK do navegador pode detectar informações alteradas de reprodução em manifestos principais do m3u8 para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK do navegador suporta um conjunto dinâmico de perfis de taxa de bits à medida que os perfis são exibidos ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre atualizações.
seo-title: Atualização ao vivo do manifesto principal
title: Atualização ao vivo do manifesto principal
uuid: 4b918a73-dacf-465a-82d6-404c6bdb01f2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Atualização principal ao vivo{#live-master-manifest-update}

O TVSDK do navegador pode detectar informações alteradas de reprodução em manifestos principais do m3u8 para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK do navegador suporta um conjunto dinâmico de perfis de taxa de bits à medida que os perfis são exibidos ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre atualizações.

Os seguintes recursos são suportados:

* Contagem de perfis (aumentando ou diminuindo)
* Taxas de bits de perfil (sobrepostas ou não sobrepostas)
* Perfis com URLs nos mesmos servidores (ou diferentes)
* Qualquer estrutura de failover

Todas as seguintes condições devem ser cumpridas:

* O fluxo é ao vivo.
* Tanto a hora quanto a tag mudam.
* Todas as informações de execução permanecem as mesmas (exceto que os URLs podem variar).
* As informações de acesso do DRM permanecem as mesmas.
* Os segmentos são empacotados ao redor dos mesmos PTS e limites de quadros em um pequeno intervalo de erros.

