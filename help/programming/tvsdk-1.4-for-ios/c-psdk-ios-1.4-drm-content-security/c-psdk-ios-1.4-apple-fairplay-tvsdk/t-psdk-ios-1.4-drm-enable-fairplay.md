---
description: Você pode implementar a transmissão FairPlay da Apple, que é a solução DRM da Apple, em seus aplicativos TVSDK.
title: Habilitar o Apple FairPlay em aplicativos TVSDK
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Habilitar o Apple FairPlay em aplicativos TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Você pode implementar a transmissão FairPlay da Apple, que é a solução DRM da Apple, em seus aplicativos TVSDK.

1. Criar o Carregador de Recursos do Cliente FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Para obter mais informações, consulte [Apple FairPlay em aplicativos TVSDK](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Siga as instruções da caixa de diálogo *Guia do programa de streaming FairPlay* ( *FairPlayStreaming_PG.pdf*), que está incluído em [SDK do servidor FairPlay para desenvolvimento de um aplicativo com reconhecimento de FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   A variável `resourceLoader:shouldWaitForLoadingOfRequestedResource` é equivalente ao que está em `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >No cenário do servidor de licenças ExpressPlay, para reproduzir o conteúdo, altere o esquema de URL no URL de solicitação de licença do servidor ExpressPlay FairPlay de `skd://` para `https://` (ou `https://`).

1. Registre o *FairPlay* Carregador de Recursos do Cliente com `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Se você criou seu próprio servidor de licenças FairPlay, ou se estiver usando um servidor de licenças FairPlay de terceiros, consulte o fornecedor do servidor de licenças para determinar o URL do servidor de licenças, a formatação e quaisquer outros requisitos.
