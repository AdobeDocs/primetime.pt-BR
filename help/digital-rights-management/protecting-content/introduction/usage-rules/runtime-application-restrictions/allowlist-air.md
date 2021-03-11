---
title: Lista de permissões por aplicativos DRM do Primetime com permissão para reproduzir conteúdo protegido
description: Lista de permissões por aplicativos DRM do Primetime com permissão para reproduzir conteúdo protegido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Lista de permissões por aplicativos DRM do Primetime com permissão para reproduzir conteúdo protegido {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Uma lista de permissões especifica os aplicativos AIR, iOS e Android que têm permissão para reproduzir conteúdo. Ela também especifica IDs de aplicativos do AIR e iOS, versão mínima, versão máxima e ID do editor.

Exemplo de caso de uso: Use essa regra para limitar a reprodução a um aplicativo específico ou para controlar a versão do aplicativo que pode acessar o conteúdo.

>[!NOTE]
>
>Se você usar o Adobe Flash Builder para criar aplicativos protegidos, certifique-se de não implantar o aplicativo no modo de Depuração. Quando você implanta um aplicativo no modo de Depuração, o Flash Builder anexa `.debug` à ID do aplicativo AIR, o que faz com que a funcionalidade do lista de permissões no DRM do Primetime se comporte inesperadamente.
