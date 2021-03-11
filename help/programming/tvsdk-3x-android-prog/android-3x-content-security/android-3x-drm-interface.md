---
description: O elemento principal do lado do cliente da solução DRM do Primetime é o Gerenciador de DRM. O aplicativo de amostra incluído no Android SDK também inclui uma classe DRMHelper que pode ser usada para facilitar a implementação de determinadas operações de DRM.
title: Visão geral da interface DRM do Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Visão geral da interface DRM do Primetime {#primetime-drm-interface-overview}

O elemento principal do lado do cliente da solução DRM do Primetime é o Gerenciador de DRM. O aplicativo de amostra incluído no Android SDK também inclui uma classe `DRMHelper` que pode ser usada para facilitar a implementação de determinadas operações de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

Para obter mais informações, consulte o código do reprodutor de amostra DRM incluído no pacote TVSDK.

Estes são os elementos de API mais importantes para trabalhar com DRM:

* Uma referência no reprodutor de mídia ao objeto do gerenciador de DRM que implementa o subsistema de DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Essa API retornará um objeto `DRMManager` válido somente após o acionamento de `MediaPlayerEvent.DRM_METADATA`. Se você chamar `getDRMManager()` antes que esse evento seja acionado, ele poderá retornar NULL.

* A classe auxiliar `DRMHelper`, que é útil ao implementar workflows de DRM.
* Um método de carregador de metadados `DRMHelper`, que carrega metadados DRM quando está localizado em um URL separado da mídia.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Um método `DRMHelper` para verificar os metadados de DRM e determinar se a autenticação é necessária.

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

Para obter mais informações sobre DRM, consulte a [documentação de DRM](https://helpx.adobe.com/primetime/user-guide.html).
