---
description: nulo
seo-description: nulo
seo-title: Lista de bloqueios dos tempos de execução do aplicativo
title: Lista de bloqueios dos tempos de execução do aplicativo
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Lista de bloqueios dos tempos de execução do aplicativo {#blocklist-of-application-runtimes}

A lista de bloqueios dos tempos de execução do aplicativo especifica a versão do cliente Primetime ou do Flash Runtime que não pode acessar o conteúdo. Especifique o tempo de execução restrito (Flash Player, AIR ou iOS), a plataforma e a versão.

Exemplo de caso de uso: Semelhante à lista de bloqueios Primetime DRM Client, a versão mais recente dos tempos de execução do Flash Player, AIR ou iOS pode ser especificada como a versão mínima necessária para a aquisição de licença e reprodução de conteúdo.

Você pode identificar o tempo de execução do aplicativo por qualquer um dos atributos suportados nas versões do cliente Primetime DRM, além dos seguintes atributos:

| **Atributo** | **Valores suportados** | **Critérios de correspondência** | **Descrição** |
|---|---|---|---|
| Aplicativo | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Correspondência exata | Identifica o nome do tempo de execução do aplicativo. |

