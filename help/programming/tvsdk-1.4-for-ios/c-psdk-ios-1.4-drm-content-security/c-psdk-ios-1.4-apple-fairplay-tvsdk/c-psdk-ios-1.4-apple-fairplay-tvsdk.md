---
description: Para implementar o FairPlay Streaming no aplicativo TVSDK, você precisa gravar um Resource Loader, que envia uma solicitação de aquisição de licença para o servidor FairPlay Streaming.
title: Apple FairPlay em aplicativos TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Apple FairPlay em aplicativos TVSDK  {#apple-fairplay-in-tvsdk-applications}

Para implementar o FairPlay Streaming no aplicativo TVSDK, você precisa gravar um Resource Loader, que envia uma solicitação de aquisição de licença para o servidor FairPlay Streaming.

O código do Carregador de recursos é responsável pelas seguintes tarefas:

1. Determine para onde enviar a solicitação de aquisição de licença.
1. Formate a solicitação.
1. Forneça as informações necessárias ao servidor, para que ele possa decidir se a solicitação deve ser permitida.

Por exemplo, se você estiver usando o Adobe Primetime Cloud DRM habilitado pela ExpressPlay, o Carregador de recursos enviará a solicitação para:

```
https://fp-gen.service.expressplay.com
```

O Carregador de Recursos formata a solicitação e anexa um token ExpressPlay que autoriza a reprodução ao URL. Ao adquirir o token ExpressPlay, há várias opções a serem consideradas. Essas opções são determinadas pela maneira como você empacotou o conteúdo.

Ao empacotar o conteúdo, o empacotador insere `skd:` URLs no manifesto M3U8. Depois que a variável `skd:` entrada, é possível colocar quaisquer dados no manifesto. É possível usar esses dados no código do aplicativo para concluir as tarefas listadas acima. Por exemplo, você pode usar `skd:{content_id}` para que seu aplicativo possa determinar a ID do conteúdo que está sendo reproduzido e solicitar um token para esse conteúdo específico. Você também pode, por exemplo, usar `skd:{entitlement_server_url}?cid={content_id}`, para que seu aplicativo não precise ter o URL do servidor de direitos codificado.

Talvez você não precise de nenhuma informação em seu `skd:` URL se, quando a reprodução começar, você já souber a ID de conteúdo por meio de outros canais. O segundo exemplo é uma solução ideal para testar sua configuração, mas você também pode usá-lo em um ambiente de produção.

>[!TIP]
>
>Você determina o formato de `skd:`.

Seu conteúdo é obtido usando o `skd:` protocolo, mas sua solicitação de licença usa `https:`. As opções mais comuns para lidar com esses protocolos são:

* **Teste inicial de reprodução completa** Ao empacotar o conteúdo, selecione uma `skd:` URL. Ao testar seu aplicativo, adquira manualmente uma licença do ExpressPlay e codifique a licença (um `https:` URL) e URL de conteúdo no seu carregador.

  Por exemplo:

  ```
  NSString* const PLAYLIST_URL =  
    @"https://{your_content_URL}/{your_manifest}.m3u8"; 
  NSString* const EXPRESSPLAY_TOKEN =  
    @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
      ExpressPlayToken={copy_your_token_to_here}";
  ```

* **A maioria dos outros casos** Ao empacotar o conteúdo, selecione uma `skd:` URL que representa exclusivamente a ID do conteúdo. No carregador, analise a variável `skd:` Envie-o ao servidor para adquirir um token e use o token resultante como o URL.

  Por exemplo:

  ```
  - (BOOL)resourceLoader:(AVAssetResourceLoader *)resourceLoader  
        shouldWaitForLoadingOfRequestedResource:(AVAssetResourceLoadingRequest *)loadingRequest { 
      NSURL *url = [[loadingRequest request] URL]; 
      if (![[url scheme] isEqual:@"skd"]) 
          return NO; 
  
      NSString *strUrl = [url absoluteString]; 
      NSLog(@"url is: %@", strUrl); 
  
      strUrl = [strUrl stringByReplacingOccurrencesOfString:@"skd://" withString:@"https://"]; 
  
      NSData *assetId; 
  
      NSData *requestBytes; 
      NSError* error = nil; 
      BOOL handled = NO; 
  
      NSData  *responseData = nil; 
  
      assetId = getMyAssetIdentifierFromURL(url); 
  
      /* Usecase 1: "On Premise Fairplay Server" 
       * Set the strUrl to the OnPremise Fairplay Server Url. The OnPremise Fairplay  
       * Server Url is either hardcoded in the App or derived from strUrl. 
       */ 
  #if 0  
      // Insert your use case 1 codes here: 
      // strUrl = getOnPremiseServerUrl(strUrl, assetId); 
  #endif // 
  
      /* Usecase 2: The strUrl is the entitlement server. 
       * Send assetId to the entitlement server; if the user is allowed to playback  
       * the content, the entitlement server will send back an ExpressPlay Token Url. 
       */ 
  
  #if 0 
      // The hardcoded SEES server: 
      strUrl = @"https://10.0.248.85:8080/sees/SEESServlet"; 
  
      // You can use the following code to simulate a device binding entitlement  
      // request:  
      // First, invoke getExpressPlayTokenUrlFromEntilementServer with  
      // bEnforceDeviceID set to false. When you play the content, the device_id  
      // will be registered on the ExpressPlay Server.  Now change code to set  
      // bEnforceDeviceID to true, and rerun the program. The ExpressPlay token  
      // sent back by the SEES server will be device bound. 
  
      // The strUrl returned below is the ExpressPlay Token URL. 
      strUrl = getExpressPlayTokenUrlFromEntilementServer(strUrl, assetId, true, &error); 
  #endif 
  
      /* Usecase 3: The strUrl is already the ExpressPlay Token Url. 
       */ 
  
      // Read in the certificate 
      NSLog(@"Get Application Certificate"); 
      NSString* certPath = [[NSBundle mainBundle] pathForResource:@"my_certificate.cer"  
                                                           ofType:nil]; 
  
      NSData *appCert = [NSData dataWithContentsOfFile:certPath]; 
  
      // To create the request blob for the server: 
      requestBytes = [loadingRequest streamingContentKeyRequestDataForApp: appCert 
                                                        contentIdentifier:assetId  
                                                                  options:nil  
                                                                    error:&error]; 
      if (requestBytes == nil) { 
          NSLog(@"Error creating server request: %@", error); 
          return false; 
      } 
      // Per the specification, send requestBytes along with the assetId to the Key 
      // Server and obtain the response. 
      NSError *err; 
  
      responseData = getCKCFromExpressPlayService( strUrl, requestBytes, assetId, &err); 
  
      if (responseData != nil) { 
          NSLog(@"Get response data: "); 
          [loadingRequest finishLoadingWithResponse:nil  
                                               data:(NSData *)responseData 
                                           redirect:nil]; 
      } 
      else { 
          [loadingRequest finishLoadingWithError:err]; 
          NSLog(@"bad key response"); 
      } 
      handled = YES; 
  bail: 
      return handled; 
  
  }
  ```

## Habilitar o Apple FairPlay em aplicativos TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Você pode implementar a transmissão FairPlay da Apple, que é a solução DRM da Apple, em seus aplicativos TVSDK.

1. Criar o Carregador de Recursos do Cliente FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Para obter mais informações, consulte [Apple FairPlay em aplicativos TVSDK](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

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
