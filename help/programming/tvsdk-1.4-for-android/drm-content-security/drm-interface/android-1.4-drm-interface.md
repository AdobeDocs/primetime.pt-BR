---
description: Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução de DRM integrada do Primetime com Adobe.
seo-description: Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução de DRM integrada do Primetime com Adobe.
seo-title: Visão geral da interface do Primetime DRM
title: Visão geral da interface do Primetime DRM
uuid: 71479464-8356-4732-9774-da9f6084e6ad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# Visão geral {#primetime-drm-interface-overview}

Você pode usar os recursos do sistema Primetime Digital Rights Management (DRM) para fornecer acesso seguro ao seu conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa à solução de DRM integrada do Primetime com Adobe.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Consulte seu representante de Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais Primetime (DRM) é o Gerenciador de DRM. O aplicativo de amostra incluído no Android SDK inclui uma classe `DRMHelper` que demonstra como facilitar a implementação de determinadas operações de DRM.

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao seu conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

Consulte o código do player de amostra de DRM incluído no pacote TVSDK.

Esses são os elementos de API mais importantes para trabalhar com DRM:

* Uma referência no player de mídia ao objeto do gerenciador DRM que implementa o subsistema DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Essa API retornará um objeto `DRMManager` válido somente depois que `MediaPlayerEvent.DRM_METADATA` for acionado. Se você chamar `getDRMManager()` antes que esse evento seja acionado, ele poderá retornar NULL.

* A classe auxiliar `DRMHelper`, que é útil ao implementar workflows DRM.

   Você pode ver `DRMHelper` em `ReferencePlayer`.

* Um método `DRMHelper` de carregador de metadados, que carrega os metadados DRM quando estão localizados em um URL separado da mídia.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Um método `DRMHelper` para verificar os metadados do DRM para determinar se a autenticação é necessária.

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

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

Elementos adicionais relevantes da API:

* [com.adobe.ave.drm.DRMManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obter mais informações sobre o DRM, consulte a [documentação do Adobe Primetime DRM](https://helpx.adobe.com/primetime/user-guide.html).
