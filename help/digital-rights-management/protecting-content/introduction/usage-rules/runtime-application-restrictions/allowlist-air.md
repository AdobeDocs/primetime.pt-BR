---
description: nulo
seo-description: nulo
seo-title: Permitir lista para aplicativos DRM Primetime com permissão para reproduzir conteúdo protegido
title: Permitir lista para aplicativos DRM Primetime com permissão para reproduzir conteúdo protegido
uuid: 23dd4faf-7992-4ee9-97ce-c6004ee995c2
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Permitir lista para aplicativos DRM Primetime com permissão para reproduzir conteúdo protegido{#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Uma lista de permissões especifica os aplicativos AIR, iOS e Android que têm permissão para reproduzir conteúdo. Ela também especifica IDs de aplicativos AIR e iOS, versão mínima, versão máxima e ID do editor.

Exemplo de caso de uso: Use essa regra para limitar a reprodução a um aplicativo específico ou para controlar a versão do aplicativo que pode acessar o conteúdo.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Se você usar o Adobe Flash Builder para criar aplicativos protegidos, certifique-se de não implantar o aplicativo no modo de Depuração. Quando você implanta um aplicativo no modo de Depuração, o Flash Builder anexa `.debug` ao ID da aplicação AIR, o que faz com que a funcionalidade permitida na DRM do Primetime se comporte inesperadamente.

