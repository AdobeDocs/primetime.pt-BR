---
description: Você pode usar o Adobe Offline packager para preparar o conteúdo para qualquer solução DRM compatível com Primetime DRM, fornecida pela ExpressPlay.
title: Primetime Packager / Cloud DRM / TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

Você pode usar o Adobe Offline packager para preparar o conteúdo para qualquer solução DRM compatível com Primetime DRM, fornecida pela ExpressPlay.

Esse conjunto de instruções pressupõe que você já tenha configurado uma conta de administrador do ExpressPlay: [Início rápido do Primetime DRM Cloud](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. Escolha a infraestrutura a ser usada para empacotar seu conteúdo. O Primetime Packager é compatível com o empacotamento de conteúdo baseado em linha de comando e configuração para uso com os DRMs FairPlay, Widevine e PlayReady. Os seguintes formatos e criptografia são compatíveis no TVSDK (com mais no pipeline):

   * DASH (CENC) / PlayReady, Widevine - Para HTML5
   * HLS / FairPlay, Acesso - Para iOS

1. Escolha um KMS (Key Management System):

   * Use o KMS do ExpressPlay ( [Armazenamento de chaves do ExpressPlay](https://www.expressplay.com/developer/key-storage/)); esse sistema gerencia suas chaves de conteúdo por meio da RESTful API do ExpressPlay.

      ou...

   * Configure seu próprio KMS. Crie um banco de dados de chaves de conteúdo, selecionável pela ID de conteúdo.

      Em ambos os casos, o KMS gerencia um suprimento de chaves de conteúdo, com cada chave com uma ID de conteúdo associada.

1. Compacte seu conteúdo. Com o Primetime Packager, você pode empacotar um conteúdo para uma solução DRM específica ou para várias soluções DRM.

   Os seguintes comandos de exemplo mostram alguns exemplos de conteúdo de empacotamento para diferentes soluções de DRM:

   * [Widevine com o Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19)  (gera arquivo MPD):

      ```
      java -jar OfflinePackager.jar \ 
        -in_path [ 
        <your_content.mp4>] \ 
        -out_type dash \ 
        -out_path [ 
        <your_out_file_path>] \ 
        -drm \ 
        -drm_sys WIDEVINE \ 
        -key_file_path "creds/widevine_key.bin" \ 
        -widevine_key_id [ 
        <some_keyID>] \ 
        -widevine_content_id [ 
        <some_content-ID] \ 
        -widevine_header provider:intertrust#content_id:2a
      ```

   * [FairPlay com Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20)  (gera um arquivo M3U8):

      ```
      java -jar OfflinePackager.jar  
        -in_path [ 
        <your_content.mp4>]  
        -out_type hls  
        -out_path [ 
        <your_out_file_path>]  
        -drm  
        -drm_sys FAIRPLAY  
        -key_file_path "creds/fairplay_key.bin"  
        -key_url "user_provided_value"
      ```

      >[!NOTE]
      >
      >O valor `key_url` é copiado como está no arquivo M3U8.

1. Crie um &quot;servidor storefront&quot;.

       O servidor storefront precisa lidar com as seguintes operações:
   
   1. Seleção de cliente do conteúdo. Essa implementação precisa incluir um terminal para que os clientes solicitem um token de conteúdo para uma ID de conteúdo específica.
   1. Direito ao cliente
   1. Solicitações de token de licença (ExpressPlay) do cliente ( [Solicitação de token de licença do ExpressPlay / referência de resposta](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. Crie seu cliente.

       O cliente deve incluir uma chamada para o servidor da loja. O Adobe recomenda que o cliente chame a loja depois que o usuário selecionar algum conteúdo e depois que o usuário for autenticado. Em seguida, passe o token retornado do ExpressPlay para o seu player para usar em solicitações de licença. As introduções para implementar o componente DRM de seus players estão aqui:
   
   * [TVSDK do navegador para HTML5](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Com o token de licença em mãos, o cliente agora pode derivar o URL da solicitação do token e fazer a solicitação de licença para ExpressPlay e, em seguida, reproduzir o conteúdo selecionado para o usuário.
