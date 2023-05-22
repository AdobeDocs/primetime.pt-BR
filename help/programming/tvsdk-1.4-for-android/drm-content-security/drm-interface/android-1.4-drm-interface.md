---
description: Você pode usar os recursos do sistema de Digital Rights Management do Primetime (DRM) para fornecer acesso seguro ao conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa para a solução de DRM Primetime integrada do Adobe.
title: Visão geral da interface DRM do Primetime
exl-id: 2f6e50e6-39f0-4939-bb9b-6c46e34bab7e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Visão geral {#primetime-drm-interface-overview}

Você pode usar os recursos do sistema de Digital Rights Management do Primetime (DRM) para fornecer acesso seguro ao conteúdo de vídeo. Como alternativa, você pode usar soluções de DRM de terceiros como uma alternativa para a solução de DRM Primetime integrada do Adobe.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Consulte seu representante de Adobe para obter as informações mais atualizadas sobre a disponibilidade de soluções de DRM de terceiros.

O elemento principal do lado do cliente do sistema de gerenciamento de direitos digitais (DRM) do Primetime é o Gerenciador de DRM. O aplicativo de amostra incluído com o Android SDK inclui um `DRMHelper` que demonstra como facilitar a implementação de determinadas operações de DRM.

O Primetime DRM fornece um fluxo de trabalho escalável e eficiente para implementar a proteção de conteúdo em aplicativos TVSDK. Você protege e gerencia os direitos ao conteúdo de vídeo criando uma licença para cada arquivo de mídia digital.

Consulte o código do reprodutor de amostra DRM incluído no pacote TVSDK.

Estes são os elementos de API mais importantes para trabalhar com DRM:

* Uma referência no reprodutor de mídia ao objeto gerenciador de DRM que implementa o subsistema de DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Essa API retornará um válido `DRMManager` somente após o `MediaPlayerEvent.DRM_METADATA` foi acionado. Se você chamar `getDRMManager()` antes de esse evento ser disparado, ele pode retornar NULL.

* A variável `DRMHelper` classe auxiliar, que é útil ao implementar workflows DRM.

   Você pode ver `DRMHelper` in `ReferencePlayer`.

* A `DRMHelper` método do carregador de metadados, que carrega metadados de DRM quando está localizado em um URL separado da mídia.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* A `DRMHelper` para verificar os metadados de DRM para determinar se a autenticação é necessária.

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

Para obter mais informações sobre DRM, consulte a [Documentação do Adobe Primetime DRM](https://helpx.adobe.com/primetime/user-guide.html).
