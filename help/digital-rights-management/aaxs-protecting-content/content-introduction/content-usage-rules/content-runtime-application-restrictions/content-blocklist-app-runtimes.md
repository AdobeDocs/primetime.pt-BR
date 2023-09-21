---
title: Lista de bloqueios de tempos de execução de aplicativo impedidos de acessar conteúdo protegido
description: Lista de bloqueios de tempos de execução de aplicativo impedidos de acessar conteúdo protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Lista de bloqueios de tempos de execução de aplicativo impedidos de acessar conteúdo protegido {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Especifica a versão do Primetime ou do Tempo de Execução do Flash que não pode acessar o conteúdo. Especifique o tempo de execução restrito (Flash Player, AIR ou iOS), a plataforma e a versão.

Exemplo de caso de uso: semelhante à lista de bloqueios do cliente DRM, a versão mais recente dos tempos de execução do Flash Player, AIR ou iOS pode ser especificada como a versão mínima necessária para a aquisição e a reprodução de conteúdo.

O tempo de execução da aplicação pode ser identificado por qualquer um dos atributos suportados pelas versões de cliente DRM, além dos seguintes atributos:

| **Atributo** | **Valores suportados** | **Corresponder critérios** | **Descrição** |
|---|---|---|---|
| Aplicativo | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Correspondência exata | Identifica o nome do tempo de execução do aplicativo. |
