---
description: O TVSDK do navegador pode detectar informações de reprodução alteradas em manifestos m3u8 principais para transmissão ao vivo e atualizar as informações de reprodução enquanto o fluxo está sendo reproduzido. O TVSDK do navegador é compatível com um conjunto dinâmico de perfis de taxa de bits à medida que os perfis aparecem ou desaparecem do manifesto principal, incluindo taxas de bits de perfil não sobrepostas entre as atualizações.
title: Atualização de manifesto principal em tempo real
exl-id: 2f89131c-5204-465b-8757-b47e955f5894
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Atualização de manifesto principal em tempo real{#live-master-manifest-update}

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
