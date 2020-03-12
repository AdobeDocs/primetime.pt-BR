---
description: Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.
seo-description: Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.
seo-title: Efeito na inserção e exclusão de anúncios no modo de sinalização de anúncios e combinações de metadados de anúncios
title: Efeito na inserção e exclusão de anúncios no modo de sinalização de anúncios e combinações de metadados de anúncios
uuid: 49abab49-4e52-477d-b7ed-688ee63e7473
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Efeito na inserção e exclusão de anúncios no modo de sinalização de anúncios e combinações de metadados de anúncios {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.

>[!TIP]
>
>Quando há um conflito entre os intervalos de tempo e os modos de sinalização de anúncios, o TVSDK dá prioridade aos intervalos de tempo.

A tabela a seguir fornece os detalhes sobre o modo de sinalização e os comportamentos de combinação de metadados:

**Mapa do servidor**

| **Metadados de anúncio** | **Resolvedores criados** | **`PlacementInformations`created ** | **Comportamento resultante** |
|--- |--- |--- |--- |
|  | Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos excluídos, Anúncios inseridos |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Publicidades inseridas |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, nenhum anúncio inserido |

**Casos de Manifesto**

| Metadados de anúncio | Resolvedores criados | `PlacementInformations` created | Comportamento resultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Publicidades inseridas |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Intervalos excluídos, anúncios inseridos |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, nenhum anúncio inserido |
| Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos |

**Intervalo de tempo personalizado**

| Metadados de anúncio | Resolvedores criados | `PlacementInformations` created | Comportamento resultante |
|--- |--- |--- |--- |
| Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos, nenhum anúncio inserido |
| Auditude | Auditude | Nenhum | Nenhuma publicidade inserida |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos por anúncios |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | Anúncio personalizado, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, nenhum anúncio inserido |

**Not set (padrão)**

| Metadados de anúncio | Resolvedores criados | `PlacementInformations` created | Comportamento resultante |
|--- |--- |--- |--- |
| Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos excluídos, anúncios inseridos |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Publicidades inseridas |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos por anúncios |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |