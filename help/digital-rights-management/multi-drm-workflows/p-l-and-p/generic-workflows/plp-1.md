---
description: Você pode usar o Adobe Offline Packager para preparar conteúdo para qualquer solução DRM compatível com o Primetime Cloud DRM, habilitado pelo ExpressPlay.
title: Primetime Packager / Cloud DRM / TVSDK
exl-id: 2055c18b-62de-41bf-9644-f366609e0198
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

Você pode usar o Adobe Offline Packager para preparar conteúdo para qualquer solução DRM compatível com o Primetime Cloud DRM, habilitado pelo ExpressPlay.

Este conjunto de instruções supõe que você já tenha configurado uma conta de administrador do ExpressPlay: [Início rápido da nuvem DRM do Primetime](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. Escolha a infraestrutura a ser usada para empacotar seu conteúdo. O Primetime Packager dá suporte a pacotes de conteúdo baseados em linha de comando e configuração para uso com os DRMs FairPlay, Widevine e PlayReady. Os seguintes formatos e criptografia são suportados atualmente no TVSDK (com mais no pipeline):

   * DASH (CENC) / PlayReady, Widevine - Para HTML5
   * HLS / FairPlay, Access - Para iOS

1. Escolha um Sistema de Gerenciamento de Chaves (KMS):

   * Uso do KMS do ExpressPlay ( [Armazenamento de chaves ExpressPlay](https://www.expressplay.com/developer/key-storage/)); esse sistema gerencia suas chaves de conteúdo por meio da API RESTful do ExpressPlay.

      ou...

   * Configure seu próprio KMS. Crie um banco de dados de chaves de conteúdo, selecionável pelo ID de conteúdo.

      Em ambos os casos, o KMS gerencia um fornecimento de chaves de conteúdo, com cada chave tendo uma ID de conteúdo associada.

1. Empacotar o conteúdo. Com o Primetime Packager, é possível disponibilizar um pacote de conteúdo para uma solução de DRM específica ou para várias soluções de DRM.

   Os exemplos de comandos a seguir mostram alguns exemplos de conteúdo de empacotamento para diferentes soluções de DRM:

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

   * [FairPlay com Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) (Gera um arquivo M3U8):

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
      >A variável `key_url` é copiado como está no arquivo M3U8.

1. Crie um &quot;servidor de vitrine&quot;.

       O servidor de vitrine precisa lidar com as seguintes operações:
   
   1. Seleção de conteúdo pelo cliente. Essa implementação precisa incluir um terminal para que os clientes solicitem um token de conteúdo para uma ID de conteúdo específica.
   1. Direitos do cliente
   1. Solicitações de token de licença (ExpressPlay) do cliente ( [Referência de resposta/solicitação de token de licença do ExpressPlay](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. Crie seu cliente.

       O cliente deve incluir uma chamada para o servidor da loja. O Adobe recomenda que o cliente chame a loja depois que o usuário selecionar algum conteúdo e depois que o usuário for autenticado. Em seguida, passe o token retornado do ExpressPlay para o player para usar em solicitações de licença. As introduções para implementar o componente de DRM dos seus players estão aqui:
   
   * [TVSDK do navegador para HTML5](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Com o token de licença em mãos, o cliente agora pode derivar o URL de solicitação do token e fazer a solicitação de licença para o ExpressPlay e, em seguida, reproduzir o conteúdo selecionado para o usuário.
