---
description: O serviço de reempacotamento criativo (CRS) garante que um anúncio não HLS possa ser reproduzido corretamente em fluxos HLS. O servidor de manifesto chama o CRS quando ele encontra um anúncio não HLS.
title: Visão geral dos SIR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Visão geral do CRS {#overview-of-crs}

O serviço de reempacotamento criativo (CRS) garante que um anúncio não HLS possa ser reproduzido corretamente em fluxos HLS. O servidor de manifesto chama o CRS quando ele encontra um anúncio não HLS.

>[!NOTE]
>
>Por padrão, o CRS está desativado. Para habilitar o CRS para sua conta, entre em contato com o gerente técnico de conta do Adobe.
>
>Para obter informações sobre como ativar o CRS em aplicativos TVSDK, consulte o tópico *Ativar CRS em aplicativos TVSDK* no Guia do programador para sua plataforma. Por exemplo, para Android 3.4, consulte [Ativar CRS em aplicativos TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

O CRS prepara HTTP Live Streaming (HLS) e cria para o fluxo de conteúdo e injeta pacotes ID3 para o rastreamento de anúncios do lado do cliente. Ele transcodifica arquivos MP4, FLV e WebM recebidos de servidores de anúncios de terceiros, redes de anúncios e servidores de agências para o formato HLS.

Quando a inserção de anúncio do Adobe Primetime encontra um anúncio não-HLS, ele o envia para o CRS para reempacotamento, que normalmente não demora mais do que três minutos. O CRS envia o anúncio transcodificado para o servidor CDN para uso futuro. Isso é chamado de **`just-in-time (JIT) repackaging`**. Você também pode transcodificar anúncios antes que eles sejam necessários usando a [Repackaging API](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . Isso é chamado de *`asynchronous repackaging`*.

Seu gerente de conta técnico do Adobe também pode alterar alguns comportamentos padrão do CRS se outro comportamento for mais adequado ao seu aplicativo. São eles:

* Prioridade dos formatos criativos de anúncio.

   A seção `MediaFiles` de uma resposta VAST/VMAP pode conter criações com diferentes tipos `MediaFile`. Por padrão, o servidor manifest seleciona um de acordo com um conjunto fixo de prioridades ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). O Adobe pode alterar as prioridades de sua conta.
* Duração do direcionamento do anúncio.

   O servidor manifest detecta a duração do anúncio do público-alvo na lista de reprodução de conteúdo e o envia para o CRS. O Adobe pode alterar esse comportamento para que o CRS sempre use uma duração fixa especificada para sua conta.
