---
seo-title: Bloquear lista de tempos de execução de aplicativos restritos de acesso a conteúdo protegido
title: Bloquear lista de tempos de execução de aplicativos restritos de acesso a conteúdo protegido
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: fbc175f383c850a7286b1e6e89daa027e00b29ef
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Bloquear lista de tempos de execução de aplicativos restritos de acesso a conteúdo protegido {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Especifica a versão do Primetime ou Flash Runtime que não pode acessar o conteúdo. Especifique o tempo de execução restrito (Flash Player, AIR ou iOS), a plataforma e a versão.

Exemplo de caso de uso: Semelhante à lista de blocos do DRM Client, a versão mais recente dos tempos de execução do Flash Player, do AIR ou do iOS pode ser especificada como a versão mínima exigida para aquisição de licença e reprodução de conteúdo.

O tempo de execução do aplicativo pode ser identificado por qualquer um dos atributos suportados para as versões do cliente DRM, além dos seguintes atributos:

| **Atributo** | **Valores suportados** | **Critérios de correspondência** | **Descrição** |
|---|---|---|---|
| Aplicativo | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Correspondência exata | Identifica o nome do tempo de execução do aplicativo. |

