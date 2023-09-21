---
description: Você pode marcar, excluir e substituir intervalos de tempo em fluxos de VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Diferentes combinações de modo de sinalização e metadados resultam em comportamentos diferentes.
title: Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios e combinações de metadados de anúncios {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Você pode marcar, excluir e substituir intervalos de tempo em fluxos de VOD usando diferentes modos de sinalização de anúncio e combinações de metadados de anúncio. Diferentes combinações de modo de sinalização e metadados resultam em comportamentos diferentes.

>[!TIP]
>
>Quando há um conflito entre intervalos de tempo e modos de sinalização de anúncio, o TVSDK atribui prioridade aos intervalos de tempo.

A tabela a seguir fornece os detalhes sobre o modo de sinalização e os comportamentos de combinação de metadados:

**Mapa do servidor**

| **Metadados de publicidade** | **Resolvedores Criados** | **`PlacementInformations`criado** | **Comportamento resultante** |
|--- |--- |--- |--- |
|  | Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos excluídos, anúncios inseridos |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anúncios inseridos |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos |
| Marcar | Anúncio personalizado | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, nenhum anúncio inserido |

**Indicações de manifesto**

| Metadados de publicidade | Resolvedores Criados | `PlacementInformations` criado | Comportamento resultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Anúncios inseridos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Intervalos excluídos, anúncios inseridos |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, nenhum anúncio inserido |
| Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Marcar | Anúncio personalizado | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos |

**Intervalo de tempo personalizado**

| Metadados de publicidade | Resolvedores Criados | `PlacementInformations` criado | Comportamento resultante |
|--- |--- |--- |--- |
| Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos, nenhum anúncio inserido |
| Auditude | Auditude | Nenhum | Nenhum anúncio inserido |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos por anúncios |
| Marcar | Anúncio personalizado | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | Anúncio personalizado, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, nenhum anúncio inserido |

**Não definido (padrão)**

| Metadados de publicidade | Resolvedores Criados | `PlacementInformations` criado | Comportamento resultante |
|--- |--- |--- |--- |
| Excluir | Excluir | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos excluídos |
| Excluir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos excluídos, anúncios inseridos |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anúncios inseridos |
| Substituir, Auditude | Excluir, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos substituídos por anúncios |
| Marcar | Anúncio personalizado | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
