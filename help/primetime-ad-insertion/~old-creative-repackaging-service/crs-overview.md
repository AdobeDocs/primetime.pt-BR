---
description: O serviço de reempacotamento criativo (CRS) garante que um anúncio não-HLS criativo possa ser reproduzido corretamente em fluxos HLS. O servidor de manifesto chama o CRS quando encontra um anúncio não HLS.
title: Visão geral do CRS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Visão geral do CRS {#overview-of-crs}

O serviço de reempacotamento criativo (CRS) garante que um anúncio não-HLS criativo possa ser reproduzido corretamente em fluxos HLS. O servidor de manifesto chama o CRS quando encontra um anúncio não HLS.

>[!NOTE]
>
>Por padrão, o CRS está desativado. Para habilitar o CRS para sua conta, entre em contato com o gerente técnico de conta da Adobe.
>
>Para obter informações sobre como ativar CRS em aplicativos TVSDK, consulte o *Habilitar CRS em aplicativos TVSDK* tópico no Guia do programador da sua plataforma. Por exemplo, para o Android 3.4, consulte [Habilitar CRS em aplicativos TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

O CRS prepara anúncios HTTP Live Streaming (HLS) para o fluxo de conteúdo e injeta pacotes ID3 para rastreamento de anúncios do lado do cliente. Ele transcodifica arquivos MP4, FLV e WebM recebidos de servidores de anúncios de terceiros, redes de anúncios e servidores de agências para o formato HLS.

Quando a inserção de anúncios do Adobe Primetime encontra um anúncio não HLS criativo, ele o envia para o CRS para reempacotamento, o que normalmente não leva mais de três minutos. O CRS envia o anúncio transcodificado e criativo para o servidor CDN para uso futuro. Isso é chamado de **`just-in-time (JIT) repackaging`**. Você também pode transcodificar anúncios criativos antes que eles sejam necessários usando o  [API de reempacotamento](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . Isso é chamado de *`asynchronous repackaging`*.

O gerente técnico de conta do Adobe também pode alterar alguns comportamentos padrão do CRS se outro comportamento for mais adequado ao aplicativo. São eles:

* Prioridade dos formatos criativos de anúncios.

   A variável `MediaFiles` seção de uma resposta VAST/VMAP pode conter criações com diferentes `MediaFile` tipos. Por padrão, o servidor de manifesto seleciona um de acordo com um conjunto fixo de prioridades ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). O Adobe pode alterar as prioridades da sua conta.
* Duração do público alvo do anúncio.

   O servidor de manifesto detecta a duração do anúncio de destino na lista de reprodução de conteúdo e a envia para o CRS. O Adobe pode alterar esse comportamento para que o CRS sempre use uma duração fixa especificada para sua conta.
