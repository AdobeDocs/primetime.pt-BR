---
description: O serviço de reempacotamento criativo (CRS) garante que um anúncio não HLS possa ser reproduzido corretamente nos fluxos HLS. O servidor manifest chama o CRS quando encontra um anúncio não HLS.
seo-description: O serviço de reempacotamento criativo (CRS) garante que um anúncio não HLS possa ser reproduzido corretamente nos fluxos HLS. O servidor manifest chama o CRS quando encontra um anúncio não HLS.
seo-title: Visão geral do SIR
title: Visão geral do SIR
uuid: 3ae75fa7-397f-47ba-8e3d-50543ca25458
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Visão geral do CRS {#overview-of-crs}

O serviço de reempacotamento criativo (CRS) garante que um anúncio não HLS possa ser reproduzido corretamente nos fluxos HLS. O servidor manifest chama o CRS quando encontra um anúncio não HLS.

>[!NOTE]
>
>Por padrão, o CRS está desativado. Para habilitar o CRS para sua conta, entre em contato com seu gerente técnico de conta do Adobe.
>
>Para obter informações sobre como habilitar CRS em aplicativos TVSDK, consulte o tópico *Habilitar CRS em aplicativos TVSDK* no Guia do Programador para sua plataforma. Por exemplo, para Android 3.4, consulte [Ativar CRS em aplicativos TVSDK](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

O CRS prepara o HTTP Live Streaming (HLS) e cria para o fluxo de conteúdo e injeta pacotes ID3 para o rastreamento de anúncios do cliente. Ele transcodifica arquivos MP4, FLV e WebM recebidos de servidores de anúncios de terceiros, redes de anúncios e servidores de agências para o formato HLS.

Quando a inserção de publicidade da Adobe Primetime encontra um anúncio não HLS criativo, ela o envia para o CRS para reempacotamento, que geralmente não leva mais de três minutos. O CRS envia o anúncio transcodificado para o servidor CDN para uso futuro. Isso é chamado **`just-in-time (JIT) repackaging`**. Você também pode transcodificar anúncios antes que eles sejam necessários usando a [API de reempacotamento](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md). Isso é chamado *`asynchronous repackaging`*.

Seu gerente técnico de conta do Adobe também pode alterar alguns comportamentos padrão do CRS se outro comportamento for mais adequado ao seu aplicativo. São eles:

* Prioridade dos formatos de anúncio.

   A seção `MediaFiles` de uma resposta VAST/VMAP pode conter criações com diferentes tipos `MediaFile`. Por padrão, o servidor manifest seleciona um de acordo com um conjunto fixo de prioridades ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). O Adobe pode alterar as prioridades da sua conta.
* Duração do público alvo do anúncio.

   O servidor manifest detecta a duração do anúncio do público alvo na lista de reprodução do conteúdo e o envia para o CRS. O Adobe pode alterar esse comportamento para que o CRS sempre use uma duração fixa especificada para sua conta.
