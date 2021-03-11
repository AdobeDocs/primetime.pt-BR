---
title: Lista de bloqueios de tempos de execução de aplicativos restritos de acesso a conteúdo protegido
description: Lista de bloqueios de tempos de execução de aplicativos restritos de acesso a conteúdo protegido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Lista de bloqueios de tempos de execução do aplicativo restritos ao acesso a conteúdo protegido {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Especifica a versão do Primetime ou do Flash Runtime que não pode acessar o conteúdo. Especifique o tempo de execução restrito (Flash Player, AIR ou iOS), a plataforma e a versão.

Exemplo de caso de uso: Semelhante à lista de bloqueios do cliente DRM, a versão mais recente dos tempos de execução do Flash Player, do AIR ou do iOS pode ser especificada como a versão mínima necessária para aquisição de licença e reprodução de conteúdo.

O tempo de execução do aplicativo pode ser identificado por qualquer um dos atributos suportados para versões de clientes DRM, além dos seguintes atributos:

| **Atributo** | **Valores compatíveis** | **Corresponder aos critérios** | **Descrição** |
|---|---|---|---|
| Aplicativo | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Correspondência exata | Identifica o nome do tempo de execução do aplicativo. |
