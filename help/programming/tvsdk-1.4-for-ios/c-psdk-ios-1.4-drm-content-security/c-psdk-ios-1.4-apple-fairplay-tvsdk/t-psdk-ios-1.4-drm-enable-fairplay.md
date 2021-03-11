---
description: Você pode implementar o Apple FairPlay Streaming, que é a solução DRM da Apple, em seus aplicativos TVSDK.
title: Ativar o Apple FairPlay em aplicativos TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Habilite o Apple FairPlay em aplicativos TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Você pode implementar o Apple FairPlay Streaming, que é a solução DRM da Apple, em seus aplicativos TVSDK.

1. Crie seu Leitor de Recursos do Cliente do FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Para obter mais informações, consulte [Apple FairPlay em aplicativos TVSDK](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Siga as instruções em *FairPlay Streaming Program Guide* ( *FairPlayStreaming_PG.pdf*), que está incluído em [FairPlay Server SDK para Desenvolvimento de um Aplicativo Sensível a FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   O método `resourceLoader:shouldWaitForLoadingOfRequestedResource` é equivalente ao que está em `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >No cenário do servidor de licenças do ExpressPlay, para reproduzir conteúdo, altere o esquema de URL no URL de solicitação de licença do servidor do ExpressPlay FairPlay de `skd://` para `https://` (ou `https://`).

1. Registre o *FairPlay* Customer Resource Loader com `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Se você escreveu seu próprio servidor de licenças do FairPlay ou estiver usando um servidor de licenças do FairPlay de terceiros, consulte o fornecedor do servidor de licenças para determinar o URL, a formatação e quaisquer outros requisitos do servidor de licenças.
