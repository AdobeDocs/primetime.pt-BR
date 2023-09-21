---
description: O TVSDK do navegador pode detectar informações de reprodução alteradas em manifestos m3u8 principais para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK do navegador é compatível com um conjunto dinâmico de perfis de taxa de bits à medida que os perfis aparecem ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre as atualizações.
title: Atualização ao vivo do manifesto principal
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Atualização ao vivo do manifesto principal{#live-master-manifest-update}

O TVSDK do navegador pode detectar informações de reprodução alteradas em manifestos m3u8 principais para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK do navegador é compatível com um conjunto dinâmico de perfis de taxa de bits à medida que os perfis aparecem ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre as atualizações.

Os seguintes recursos são compatíveis:

* Contagem de perfis (aumentando ou diminuindo)
* Taxas de bits de perfil (sobreposição ou não sobreposição)
* Perfis com URLs nos mesmos servidores (ou diferentes)
* Qualquer estrutura de failover

Todas as seguintes condições devem ser atendidas:

* O fluxo está ativo.
* A hora e a tag mudam.
* Todas as informações de representação permanecem as mesmas (exceto que os URLs podem variar).
* As informações de acesso do DRM permanecem inalteradas.
* Segmentos são empacotados ao redor do mesmo PTS e limites de quadro em um pequeno intervalo de erro.
