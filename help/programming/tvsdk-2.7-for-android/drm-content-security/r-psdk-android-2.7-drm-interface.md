---
description: O elemento principal do lado do cliente da solução de DRM do Primetime é o Gerenciador de DRM. O aplicativo de exemplo incluído com o Android SDK também inclui uma classe DRMHelper que pode ser usada para facilitar a implementação de determinadas operações de DRM.
title: Visão geral da interface DRM do Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Visão geral da interface DRM do Primetime {#primetime-drm-interface-overview}

O elemento principal do lado do cliente da solução de DRM do Primetime é o Gerenciador de DRM. O aplicativo de exemplo incluído com o Android SDK também inclui uma classe DRMHelper que pode ser usada para facilitar a implementação de determinadas operações de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

Para obter mais informações, consulte o código do reprodutor de amostra do DRM incluído no pacote TVSDK.

Estes são os elementos mais importantes da API para trabalhar com DRM:

* Uma referência no reprodutor de mídia ao objeto gerenciador de DRM que implementa o subsistema de DRM:

  ```java
  MediaPlayer.getDRMManager();
  ```

  >[!TIP]
  >
  >Essa API retornará um válido `DRMManager` somente após o `MediaPlayerEvent.DRM_METADATA` foi acionado. Se você chamar `getDRMManager()` antes de esse evento ser disparado, ele pode retornar NULL.

* A variável `DRMHelper` classe auxiliar, que é útil ao implementar workflows DRM.
* A `DRMHelper` método do carregador de metadados, que carrega metadados de DRM quando está localizado em um URL separado da mídia.

  ```java
  public static void loadDRMMetadata(final DRMManager drmManager,  
     final String drmMetadataUrl,  
     final DRMLoadMetadataListener loadMetadataListener);
  ```

* A `DRMHelper` para verificar os metadados de DRM e determinar se a autenticação é necessária.

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

* Eventos que notificam seu aplicativo sobre várias atividades e status de DRM.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obter mais informações sobre DRM, consulte a [Documentação do DRM](https://helpx.adobe.com/primetime/user-guide.html).
