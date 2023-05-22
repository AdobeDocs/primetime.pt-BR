---
title: Lista de permissões para aplicativos do Adobe® Primetime com permissão para reproduzir conteúdo protegido
description: Lista de permissões para aplicativos do Adobe® Primetime com permissão para reproduzir conteúdo protegido
copied-description: true
exl-id: 56004a0f-118c-42f3-869b-2cc1c91ee544
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
