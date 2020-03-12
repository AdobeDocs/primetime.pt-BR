---
description: O elemento principal do cliente da solução Primetime DRM é o Gerenciador de DRM. O aplicativo de amostra incluído no Android SDK também inclui uma classe DRMHelper que pode ser usada para facilitar a implementação de determinadas operações DRM.
seo-description: O elemento principal do cliente da solução Primetime DRM é o Gerenciador de DRM. O aplicativo de amostra incluído no Android SDK também inclui uma classe DRMHelper que pode ser usada para facilitar a implementação de determinadas operações DRM.
seo-title: Visão geral da interface do Primetime DRM
title: Visão geral da interface do Primetime DRM
uuid: d77a98c8-c1f5-4fe3-8d0b-3d21e288f228
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Visão geral da interface do Primetime DRM {#primetime-drm-interface-overview}

O elemento principal do cliente da solução Primetime DRM é o Gerenciador de DRM. O aplicativo de amostra incluído no Android SDK também inclui uma classe DRMHelper que pode ser usada para facilitar a implementação de determinadas operações DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao seu conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

Para obter mais informações, consulte o código do player de amostra de DRM incluído no pacote TVSDK.

Estes são os elementos de API mais importantes para trabalhar com DRM:

* Uma referência no player de mídia ao objeto do gerenciador DRM que implementa o subsistema DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Essa API retornará um `DRMManager` objeto válido somente depois que o objeto `MediaPlayerEvent.DRM_METADATA` for acionado. Se você ligar `getDRMManager()` antes que esse evento seja acionado, ele poderá retornar NULL.

* A classe `DRMHelper` helper, que é útil ao implementar fluxos de trabalho de DRM.
* Um método `DRMHelper` de carregador de metadados, que carrega metadados DRM quando está localizado em um URL separado da mídia.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Um `DRMHelper` método para verificar os metadados do DRM e determinar se a autenticação é necessária.

   ```java
   /** 
   * Return whether authentication is needed for the provided 
   * DRMMetadata. 
   * 
   * @param drmMetadata 
   * The desired DRMMetadata on which to check whether auth is needed. 
   * @return whether authentication is required for the provided metadata 
   */ 
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

* `DRMHelper` para executar a autenticação.

   ```java
   /** 
   * Helper method to perform DRM authentication. 
   * 
   * @param drmManager 
   * the DRMManager, used to perform the authentication. 
   * @param drmMetadata 
   * the DRMMetadata, containing the DRM specific information. 
   * @param authenticationListener 
   * the listener, on which the user can be notified about the 
   * authentication process status. 
   * @param authUser 
   * the DRM username provider by the user. 
   * @param authPass 
   * the DRM password provided by the user. 
   */ 
   public static void performDrmAuthentication(final DRMManager drmManager,  
   final DRMMetadata drmMetadata,  
   final String authUser,  
   final String authPass,  
   final DRMAuthenticationListener authenticationListener);
   ```

* Eventos que notificam seu aplicativo sobre várias atividades e status do DRM.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obter mais informações sobre o DRM, consulte a documentação [do](https://helpx.adobe.com/primetime/user-guide.html)DRM.
