---
description: Para disponibilizar as legendas ocultas para o player cliente, ative-as. O usuário pode ativar ou desativar legendas ocultas e selecionar a formatação.
seo-description: Para disponibilizar as legendas ocultas para o player cliente, ative-as. O usuário pode ativar ou desativar legendas ocultas e selecionar a formatação.
seo-title: Expor legendas ocultas
title: Expor legendas ocultas
uuid: 7057014a-b14a-4790-8f7f-37d7a1fb8194
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Expor legendas ocultas {#expose-closed-captions}

Para disponibilizar as legendas ocultas para o player cliente, ative-as. O usuário pode ativar ou desativar legendas ocultas e selecionar a formatação.

Para expor legendas ocultas:

1. Em `PTMediaPlayer` objeto, defina a `closedCaptionDisplayEnabled` propriedade.

   Se o usuário ativou legendas ocultas, essa etapa exibe o texto.

   >[!NOTE]
   >
   >O usuário cliente ativa ou desativa as legendas ocultas usando as Configurações de acessibilidade do iOS, e essas configurações também fornecem opções de formatação.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` está obsoleta. Use `subtitlesOptions` a propriedade de `PTMediaPlayerItem`. Consulte [Expor legendas](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) para usar legendas ocultas.