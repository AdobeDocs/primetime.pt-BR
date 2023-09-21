---
title: Lista de permissões para aplicativos do Adobe® Primetime com permissão para reproduzir conteúdo protegido
description: Lista de permissões para aplicativos do Adobe® Primetime com permissão para reproduzir conteúdo protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Lista de permissões para aplicativos do Adobe® Primetime com permissão para reproduzir conteúdo protegido {#allowlist-for-adobe-primetime-applications-allowed-to-play-protected-content}

Especifica os aplicativos AIR/iOS que podem reproduzir conteúdo. Especifique a ID do aplicativo do AIR/iOS, a versão mínima, a versão máxima e a ID do editor.

Exemplo de caso de uso: use essa regra para limitar a reprodução a um aplicativo AIR/iOS específico ou para controlar qual versão pode acessar o conteúdo.

>[!NOTE]
>
>Se estiver usando o Flash Builder Adobe para criar aplicativos protegidos, certifique-se de não implantar o aplicativo no modo &quot;Depurar&quot;. Ao implantar um aplicativo no modo &quot;Depurar&quot;, o Flash Builder anexará &quot;.debug&quot; à ID do aplicativo do AIR. Isso fará com que a funcionalidade de lista de permissões no Adobe Access se comporte inesperadamente.
