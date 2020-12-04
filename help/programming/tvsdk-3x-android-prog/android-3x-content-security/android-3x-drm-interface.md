---
description: O elemento principal do cliente da solução Primetime DRM é o Gerenciador de DRM. O aplicativo de amostra incluído no Android SDK também inclui uma classe DRMHelper que pode ser usada para facilitar a implementação de determinadas operações DRM.
seo-description: O elemento principal do cliente da solução Primetime DRM é o Gerenciador de DRM. O aplicativo de amostra incluído no Android SDK também inclui uma classe DRMHelper que pode ser usada para facilitar a implementação de determinadas operações DRM.
seo-title: Visão geral da interface do Primetime DRM
title: Visão geral da interface do Primetime DRM
uuid: 9e6f6ae6-7193-40fe-bc9d-d8de33705f5d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Visão geral da interface do Primetime DRM {#primetime-drm-interface-overview}

O elemento principal do cliente da solução Primetime DRM é o Gerenciador de DRM. O aplicativo de amostra incluído no Android SDK também inclui uma classe `DRMHelper` que pode ser usada para facilitar a implementação de determinadas operações de DRM.

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
   >Essa API retornará um objeto `DRMManager` válido somente depois que `MediaPlayerEvent.DRM_METADATA` for acionado. Se você chamar `getDRMManager()` antes que esse evento seja acionado, ele poderá retornar NULL.

* A classe auxiliar `DRMHelper`, que é útil ao implementar workflows DRM.
* Um método `DRMHelper` de carregador de metadados, que carrega os metadados DRM quando estão localizados em um URL separado da mídia.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Um método `DRMHelper` para verificar os metadados do DRM e determinar se a autenticação é necessária.

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

Para obter mais informações sobre o DRM, consulte a documentação do [DRM](https://helpx.adobe.com/primetime/user-guide.html).
