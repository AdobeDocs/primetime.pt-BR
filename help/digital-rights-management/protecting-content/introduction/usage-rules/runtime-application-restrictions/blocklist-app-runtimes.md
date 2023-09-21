---
title: Lista de bloqueios de tempos de execução do aplicativo
description: Lista de bloqueios de tempos de execução do aplicativo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Lista de bloqueios de tempos de execução do aplicativo {#blocklist-of-application-runtimes}

A lista de bloqueios de tempos de execução do aplicativo especifica a versão do cliente Primetime ou do Tempo de Execução do Flash que não pode acessar o conteúdo. Especifique o tempo de execução restrito (Flash Player, AIR ou iOS), a plataforma e a versão.

Exemplo de caso de uso: assim como a lista de bloqueios de cliente do Primetime DRM, a versão mais recente dos tempos de execução do Flash Player, AIR ou iOS pode ser especificada como a versão mínima necessária para a aquisição e a reprodução de conteúdo.

Você pode identificar o tempo de execução do aplicativo por qualquer um dos atributos suportados pelas versões de cliente do Primetime DRM, além dos seguintes atributos:

| **Atributo** | **Valores suportados** | **Corresponder critérios** | **Descrição** |
|---|---|---|---|
| Aplicativo | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Correspondência exata | Identifica o nome do tempo de execução do aplicativo. |
