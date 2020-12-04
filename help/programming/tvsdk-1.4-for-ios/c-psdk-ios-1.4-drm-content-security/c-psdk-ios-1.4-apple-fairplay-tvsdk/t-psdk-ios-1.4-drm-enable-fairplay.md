---
description: Você pode implementar o streaming do Apple FairPlay, que é a solução DRM da Apple, em seus aplicativos TVSDK.
seo-description: Você pode implementar o streaming do Apple FairPlay, que é a solução DRM da Apple, em seus aplicativos TVSDK.
seo-title: Habilitar o Apple FairPlay em aplicativos TVSDK
title: Habilitar o Apple FairPlay em aplicativos TVSDK
uuid: fafffdb9-09f9-45fb-9957-3c6e95ed55f9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Habilitar o Apple FairPlay em aplicativos TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Você pode implementar o streaming do Apple FairPlay, que é a solução DRM da Apple, em seus aplicativos TVSDK.

1. Crie seu Carregador de Recursos do Cliente do FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Para obter mais informações, consulte [Apple FairPlay em aplicativos TVSDK](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Certifique-se de seguir as instruções no *FairPlay Streaming Programa Guide* ( *FairPlayStreaming_PG.pdf*), que está incluído no [FairPlay Server SDK para Desenvolvimento de um Aplicativo Sensível ao FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   O método `resourceLoader:shouldWaitForLoadingOfRequestedResource` é equivalente ao que está em `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >No cenário do servidor de licenças do ExpressPlay, para reproduzir o conteúdo, altere o esquema de URL no URL de solicitação de licença do servidor do ExpressPlay FairPlay de `skd://` para `https://` (ou `https://`).

1. Registre o *FairPlay* Carregador de Recursos do Cliente com `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Se você escreveu seu próprio servidor de licenças do FairPlay ou estiver usando um servidor de licenças do FairPlay de terceiros, consulte o fornecedor do servidor de licenças para determinar o URL, a formatação e quaisquer outros requisitos do servidor de licenças.
