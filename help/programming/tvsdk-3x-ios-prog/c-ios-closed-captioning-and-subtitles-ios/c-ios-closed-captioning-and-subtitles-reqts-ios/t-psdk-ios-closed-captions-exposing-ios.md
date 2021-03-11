---
description: Para disponibilizar legendas ocultas para o player do cliente, você deve ativá-las. O usuário pode ativar ou desativar as legendas ocultas e selecionar a formatação.
title: Expor legendas ocultas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Expor legendas ocultas {#expose-closed-captions}

Para disponibilizar legendas ocultas para o player do cliente, você deve ativá-las. O usuário pode ativar ou desativar as legendas ocultas e selecionar a formatação.

Para expor legendas ocultas:

1. No objeto `PTMediaPlayer`, defina a propriedade `closedCaptionDisplayEnabled`.

   Se o usuário ativou legendas ocultas, esta etapa exibe o texto.

   >[!NOTE]
   >
   >O usuário cliente ativa ou desativa as legendas ocultas usando as Configurações de acessibilidade do iOS, e essas configurações também fornecem opções de formatação.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` está obsoleta. Use a propriedade `subtitlesOptions` de `PTMediaPlayerItem`. Consulte [Expor legendas](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) para usar legendas ocultas.