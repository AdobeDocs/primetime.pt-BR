---
title: Lista de permissões aplicativos DRM do Primetime com permissão para reproduzir conteúdo protegido
description: Lista de permissões aplicativos DRM do Primetime com permissão para reproduzir conteúdo protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Lista de permissões aplicativos DRM do Primetime com permissão para reproduzir conteúdo protegido {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Uma lista de permissões especifica os aplicativos AIR, iOS e Android que têm permissão para reproduzir conteúdo. Também especifica as IDs de aplicativo do AIR e do iOS, a versão mínima, a versão máxima e a ID do editor.

Exemplo de caso de uso: use essa regra para limitar a reprodução a um aplicativo específico ou para controlar a versão do aplicativo que pode acessar o conteúdo.

>[!NOTE]
>
>Se você usar o Flash Builder Adobe para criar aplicativos protegidos, certifique-se de não implantar o aplicativo no modo de Depuração. Quando você implanta uma aplicação no modo de Depuração, o Flash Builder anexa `.debug` à ID do aplicativo do AIR, o que faz com que a funcionalidade de lista de permissões no Primetime DRM se comporte inesperadamente.
