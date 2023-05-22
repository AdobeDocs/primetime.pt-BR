---
description: Para disponibilizar legendas ocultas para o player do cliente, você deve ativá-las. O usuário pode ativar ou desativar as legendas ocultas e selecionar a formatação.
title: Expor legendas ocultas
exl-id: 6383a2b2-04e3-4fe1-a573-5e1f1ef486ed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Expor legendas ocultas {#expose-closed-captions}

Para disponibilizar legendas ocultas para o player do cliente, você deve ativá-las. O usuário pode ativar ou desativar as legendas ocultas e selecionar a formatação.

Para expor legendas ocultas:

1. Entrada `PTMediaPlayer` , defina o `closedCaptionDisplayEnabled` propriedade.

   Se o usuário tiver ativado as legendas ocultas, essa etapa exibirá o texto.

   >[!NOTE]
   >
   >O usuário cliente ativa ou desativa as legendas ocultas usando as Configurações de acessibilidade do iOS, que também fornecem opções de formatação.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` propriedade está obsoleta. Uso `subtitlesOptions` propriedade de `PTMediaPlayerItem`. Consulte [Expor legendas](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) para usar legendas ocultas.
