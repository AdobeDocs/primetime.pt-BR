---
title: Lista de bloqueios dos tempos de execução do aplicativo
description: Lista de bloqueios dos tempos de execução do aplicativo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Lista de bloqueios dos tempos de execução do aplicativo {#blocklist-of-application-runtimes}

A lista de bloqueios de tempos de execução do aplicativo especifica a versão do cliente Primetime ou do Flash Runtime que não pode acessar o conteúdo. Especifique o tempo de execução restrito (Flash Player, AIR ou iOS), a plataforma e a versão.

Exemplo de caso de uso: Semelhante à lista de bloqueios do cliente DRM do Primetime, a versão mais recente dos tempos de execução do Flash Player, do AIR ou do iOS pode ser especificada como a versão mínima necessária para aquisição de licença e reprodução de conteúdo.

Você pode identificar o tempo de execução do aplicativo por qualquer um dos atributos suportados pelas versões do cliente DRM do Primetime, além dos seguintes atributos:

| **Atributo** | **Valores compatíveis** | **Corresponder aos critérios** | **Descrição** |
|---|---|---|---|
| Aplicativo | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Correspondência exata | Identifica o nome do tempo de execução do aplicativo. |

