---
description: Para disponibilizar as legendas ocultas para o player cliente, ative-as. O usuário pode ativar ou desativar legendas ocultas e selecionar a formatação.
seo-description: Para disponibilizar as legendas ocultas para o player cliente, ative-as. O usuário pode ativar ou desativar legendas ocultas e selecionar a formatação.
seo-title: Expor legendas ocultas
title: Expor legendas ocultas
uuid: 209b34ca-f14e-499e-af5f-2d8c7b359ef8
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Expor legendas ocultas {#expose-closed-captions}

Para disponibilizar as legendas ocultas para o player cliente, ative-as. O usuário pode ativar ou desativar legendas ocultas e selecionar a formatação.

Para expor legendas ocultas:

1. No objeto `PTMediaPlayer`, defina a propriedade `closedCaptionDisplayEnabled`.

   Se o usuário ativou legendas ocultas, essa etapa exibe o texto.

   >[!NOTE]
   >
   >O usuário cliente ativa ou desativa as legendas ocultas usando as Configurações de acessibilidade do iOS, e essas configurações também fornecem opções de formatação.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` está obsoleta. Use a propriedade `subtitlesOptions` de `PTMediaPlayerItem`. Consulte [Expor legendas](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) para usar legendas fechadas.