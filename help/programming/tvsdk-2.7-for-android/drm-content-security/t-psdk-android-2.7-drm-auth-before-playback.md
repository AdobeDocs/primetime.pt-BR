---
description: Quando os metadados de DRM de um vídeo estão separados do fluxo de mídia, você deve autenticar antes de iniciar a reprodução.
title: Autenticação DRM antes da reprodução
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---


# Autenticação DRM antes da reprodução {#drm-authentication-before-playback}

Quando os metadados de DRM de um vídeo estão separados do fluxo de mídia, você deve autenticar antes de iniciar a reprodução.

Um ativo de vídeo pode ter um arquivo de metadados DRM associado, por exemplo:

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

Neste exemplo, você pode usar os métodos `DRMHelper` para baixar o conteúdo do arquivo de metadados DRM, analisá-lo e verificar se a autenticação DRM é necessária.

1. Use `loadDRMMetadata` para carregar o conteúdo do URL de metadados e analisar os bytes baixados em um `DRMMetadata`.

   >[!TIP]
   >
   >Esse método é assíncrono e cria seu próprio thread.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   Por exemplo:

   ```java
   DRMHelper.loadDRMMetadata(drmManager,  
                                      metadataURL,  
                                      new DRMLoadMetadataListener());
   ```

1. Notifique o usuário que essa operação é assíncrona. Convém informar o usuário sobre isso.

   Se os usuários não souberem que a operação é assíncrona, poderão se perguntar por que a reprodução ainda não foi iniciada. Você pode, por exemplo, mostrar uma roda giratória enquanto os metadados de DRM estão sendo baixados e analisados.

1. Implemente os retornos de chamada no `DRMLoadMetadataListener`.

   O `loadDRMMetadata` chama esses manipuladores de evento.

   ```java
   public interface DRMLoadMetadataListener { 
   
       public void onLoadMetadataUrlStart(); 
   
       /** 
       * @param authNeeded 
       * whether DRM authentication is needed. 
       * @param drmMetadata 
       * the parsed DRMMetadata obtained.    */ 
       public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata); 
       public void onLoadMetadataUrlError(); 
   } 
   ```

   Aqui estão detalhes adicionais sobre os manipuladores:

   * `onLoadMetadataUrlStart` detecta quando o carregamento do URL de metadados começou.
   * `onLoadMetadataUrlComplete` O detecta quando o URL de metadados terminou de ser carregado.
   * `onLoadMetadataUrlError` indica que os metadados não foram carregados.

1. Após concluir o carregamento, inspecione o objeto `DRMMetadata` para determinar se a autenticação de DRM é necessária.

   ```java
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

   Por exemplo:

   ```java
   @Override 
   public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata) {  
       Log.i(LOG_TAG + "#onLoadMetadataUrlComplete",  
             "Loaded metadata URL contents. Auth needed:" + authNeeded + "."); 
       if (!authNeeded) { 
           // Auth is not required. Start player activity.     
           showLoadingSpinner(false);     
           startPlayerActivity(ASSET_URL); 
           return; 
       } 
   } 
   ```

1. Conclua uma das seguintes tarefas:

   * Se a autenticação não for necessária, inicie a reprodução.
   * Se a autenticação for necessária, conclua a autenticação adquirindo a licença.

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
      */ 
      public static void performDrmAuthentication( 
           final DRMManager drmManager,  
           final DRMMetadata drmMetadata, 
           final String authUser,  
           final String authPass,  
           final DRMAuthenticationListener authenticationListener);
      ```

      Neste exemplo, para simplificar, o nome e a senha do usuário são explicitamente codificados:

      ```java
      DRMHelper.performDrmAuthentication(drmManager,  
                                         drmMetadata,  
                                         DRM_USERNAME,  
                                         DRM_PASSWORD, new DRMAuthenticationListener() { 
          @Override 
          public void onAuthenticationStart() { 
              Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
              // Spinner is already showing. 
          } 
          @Override 
          public void onAuthenticationError(int major,  
                                            int minor,  
                                            String errorString,  
                                            String serverErrorURL) { 
              Log.e(LOG_TAG +  
                    "#onAuthenticationError",  
                    "DRM authentication failed. " +  
                    major + " 0x" + Long.toHexString(minor)); 
              showToast(getString(R.string.drmAuthenticationError));   
              showLoadingSpinner(false); 
          } 
          @Override 
          public void onAuthenticationComplete(byte[] authenticationToken) { 
              Log.i(LOG_TAG +  
                    "#onAuthenticationComplete", "Auth successful. Launching content."); 
              showLoadingSpinner(false); 
              startPlayerActivity(ASSET_URL); 
          } 
      }); 
      ```

1. Use um ouvinte de evento para verificar o status de autenticação.

   Esse processo implica a comunicação da rede, então essa também é uma operação assíncrona.

   ```java
   public interface DRMAuthenticationListener { 
       /** 
       * Called to indicate that DRM authentication has started. 
       */ 
       public void onAuthenticationStart(); 
       /** 
       * Called to indicate that DRM authentication has been successful. 
       * 
       * @param authenticationToken 
       * the obtained token, which can be stored locally. 
       */ 
       public void onAuthenticationComplete(byte[] authenticationToken); 
       /** 
       * Called to indicate that an error occurred while performing the DRM 
       * authentication. 
       * 
       * @param major 
       * the major code. 
       * @param minorC 
       * the minor code. 
       * @param errorString 
       * the exception thrown. 
       * @param serverErrorURL 
       * the URL of the server  
       * on which the error occurred 
       */ 
       public void onAuthenticationError(int major,  
                                         int minor,  
                                         String errorString,  
                                         String serverErrorURL); 
   } 
   ```

1. Se a autenticação for bem-sucedida, inicie a reprodução.
1. Se a autenticação não for bem-sucedida, notifique o usuário e não inicie a reprodução.

   Seu aplicativo deve lidar com erros de autenticação. Falha na autenticação antes da reprodução do coloca o TVSDK em um estado de erro e a reprodução é interrompida. Seu aplicativo deve resolver o problema, redefinir o reprodutor e recarregar o recurso.
