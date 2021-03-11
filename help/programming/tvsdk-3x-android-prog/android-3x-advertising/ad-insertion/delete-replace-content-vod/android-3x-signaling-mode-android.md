---
description: Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes combinações de metadados de anúncio e modo de sinalização de anúncios. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.
title: Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncio {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Você pode marcar, excluir e substituir intervalos de tempo em fluxos VOD usando diferentes combinações de metadados de anúncio e modo de sinalização de anúncios. Combinações diferentes de modo de sinalização e metadados resultam em comportamentos diferentes.

>[!TIP]
>
>Quando há um conflito entre os intervalos de tempo e os modos de sinalização de anúncios, o TVSDK dá prioridade aos intervalos de tempo.

A tabela a seguir fornece os detalhes sobre o modo de sinalização e os comportamentos de combinação de metadados:

**Mapa do servidor**

| **Metadados de anúncio** | **Resolvedores Criados** | **`PlacementInformations`criado** | **Comportamento resultante** |
|--- |--- |--- |--- |
|  | Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos excluídos, Anúncios inseridos |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anúncios inseridos |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, nenhum anúncio inserido |

**Casos de manifesto**

| Metadados de anúncio | Resolvedores Criados | `PlacementInformations` criado | Comportamento resultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Anúncios inseridos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Intervalos excluídos, publicidades inseridas |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, nenhum anúncio inserido |
| Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos |

**Intervalo de tempo personalizado**

| Metadados de anúncio | Resolvedores Criados | `PlacementInformations` criado | Comportamento resultante |
|--- |--- |--- |--- |
| Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos, nenhum anúncio inserido |
| Auditude | Auditude | Nenhum | Nenhuma publicidade inserida |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos por anúncios |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | Anúncio personalizado, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, nenhum anúncio inserido |

**Not set (padrão)**

| Metadados de anúncio | Resolvedores Criados | `PlacementInformations` criado | Comportamento resultante |
|--- |--- |--- |--- |
| Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos excluídos, publicidades inseridas |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anúncios inseridos |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos por anúncios |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |