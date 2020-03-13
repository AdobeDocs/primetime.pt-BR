---
description: Você pode usar o empacotador offline da Adobe para preparar conteúdo para qualquer solução DRM compatível com o Primetime Cloud DRM, fornecido pelo ExpressPlay.
seo-description: Você pode usar o empacotador offline da Adobe para preparar conteúdo para qualquer solução DRM compatível com o Primetime Cloud DRM, fornecido pelo ExpressPlay.
seo-title: Primetime Packager / Cloud DRM / TVSDK
title: Primetime Packager / Cloud DRM / TVSDK
uuid: e54a0e4d-c8ea-46d4-b1b0-bed8a680f8f5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

Você pode usar o empacotador offline da Adobe para preparar conteúdo para qualquer solução DRM compatível com o Primetime Cloud DRM, fornecido pelo ExpressPlay.

Este conjunto de instruções presume que você já tenha configurado uma conta de administrador do ExpressPlay: Início rápido [da nuvem DRM do](../../../multi-drm-workflows/quick-start/quick-overview.md)Primetime.
1. Escolha a infraestrutura a ser usada para empacotar seu conteúdo. O Primetime Packager oferece suporte a pacotes de conteúdo baseados em linha de comando e configuração para uso com os DRMs FairPlay, Widevine e PlayReady. Os seguintes formatos e criptografia são suportados atualmente no TVSDK (com mais no pipeline):

   * DASH (CENC) / PlayReady, Widevine - para HTML5
   * HLS / FairPlay, Access - para iOS

1. Escolha um KMS (Key Management System):

   * Usar o KMS ( [ExpressPlay Key Storage](https://www.expressplay.com/developer/key-storage/)) do ExpressPlay; este sistema gerencia suas chaves de conteúdo por meio da RESTful API do ExpressPlay.

      ou...

   * Configure seu próprio KMS. Crie um banco de dados de chaves de conteúdo, selecionável por ID de conteúdo.

      Em ambos os casos, o KMS gerencia um suprimento de chaves de conteúdo, com cada chave com uma ID de conteúdo associada.

1. Empacote seu conteúdo. Com o Primetime Packager, é possível disponibilizar um conteúdo para uma solução DRM específica ou para várias soluções DRM.

   Os seguintes comandos de amostra mostram alguns exemplos de conteúdo de empacotamento para diferentes soluções de DRM:

   * [Widevine com Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19) (gera arquivo MPD):

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

   * [FairPlay com Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) (gera um arquivo M3U8):

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
      >O `key_url` valor é copiado como está no arquivo M3U8.

1. Crie um &quot;servidor storefront&quot;.

       O servidor storefront precisa lidar com as seguintes operações:
   
   1. Seleção de conteúdo pelo cliente. Essa implementação precisa incluir um terminal para que os clientes solicitem um token de conteúdo para uma ID de conteúdo específica.
   1. Direito ao cliente
   1. Solicitações de token de licença (ExpressPlay) do cliente (solicitação de token de licença do [ExpressPlay / referência](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md)de resposta)

1. Crie seu cliente.

       O cliente deve incluir uma chamada para seu servidor storefront. A Adobe recomenda que o cliente chame o storefront depois que o usuário selecionar algum conteúdo e depois que o usuário for autenticado. Em seguida, passe o token retornado do ExpressPlay para o player para uso em solicitações de licença. Apresentações para implementar o componente DRM dos seus players estão aqui:
   
   * [TVSDK do navegador para HTML5](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Com o token de licença em mãos, o cliente agora pode derivar o URL da solicitação do token e fazer a solicitação de licença para o ExpressPlay e, em seguida, reproduzir o conteúdo selecionado para o usuário.
