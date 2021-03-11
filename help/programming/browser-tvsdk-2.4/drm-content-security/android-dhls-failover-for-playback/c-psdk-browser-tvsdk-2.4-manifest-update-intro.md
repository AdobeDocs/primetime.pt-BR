---
description: O TVSDK do navegador pode detectar informações de reprodução alteradas em manifestos principais do m3u8 para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK do navegador oferece suporte a um conjunto dinâmico de perfis de taxa de bits conforme os perfis são exibidos ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre atualizações.
title: Atualização de manifesto principal ao vivo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Atualização de manifesto principal ao vivo{#live-master-manifest-update}

O TVSDK do navegador pode detectar informações de reprodução alteradas em manifestos principais do m3u8 para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK do navegador oferece suporte a um conjunto dinâmico de perfis de taxa de bits conforme os perfis são exibidos ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre atualizações.

Os seguintes recursos são compatíveis:

* Contagem de perfis (aumento ou diminuição)
* Taxas de bits do perfil (sobreposição ou não sobreposição)
* Perfis com URLs nos mesmos servidores (ou em servidores diferentes)
* Qualquer estrutura de failover

Todas as condições a seguir devem ser atendidas:

* O fluxo está ao vivo.
* Tanto a hora quanto a tag mudam.
* Todas as informações de representação permanecem as mesmas (exceto que os URLs podem variar).
* As informações de acesso do DRM permanecem as mesmas.
* Os segmentos são empacotados em torno do mesmo PTS e limites de quadros em um pequeno intervalo de erros.

