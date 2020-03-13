---
description: nulo
seo-description: nulo
seo-title: Lista negra dos tempos de execução do aplicativo
title: Lista negra dos tempos de execução do aplicativo
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista negra dos tempos de execução do aplicativo{#blacklist-of-application-runtimes}

A lista negra dos tempos de execução do aplicativo especifica a versão do cliente Primetime ou Flash Runtime que não pode acessar o conteúdo. Especifique o tempo de execução restrito (Flash Player, AIR ou iOS), a plataforma e a versão.

Exemplo de caso de uso: Semelhante à lista negra do Primetime DRM Client, a versão mais recente dos tempos de execução do Flash Player, do AIR ou do iOS pode ser especificada como a versão mínima exigida para aquisição de licença e reprodução de conteúdo.

Você pode identificar o tempo de execução do aplicativo por qualquer um dos atributos suportados nas versões do cliente Primetime DRM, além dos seguintes atributos:

| **Atributo** | **Valores suportados** | **Critérios de correspondência** | **Descrição** |
|---|---|---|---|
| Aplicativo | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Correspondência exata | Identifica o nome do tempo de execução do aplicativo. |

