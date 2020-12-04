---
description: Quando os metadados DRM de um vídeo são incluídos no fluxo de mídia, é possível executar a autenticação durante a reprodução.
seo-description: Quando os metadados DRM de um vídeo são incluídos no fluxo de mídia, é possível executar a autenticação durante a reprodução.
seo-title: Autenticação DRM durante a reprodução
title: Autenticação DRM durante a reprodução
uuid: b3ff8edd-a3d4-470e-8899-580eca9fff4a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Autenticação DRM durante a reprodução {#drm-authentication-during-playback}

Quando os metadados DRM de um vídeo são incluídos no fluxo de mídia, é possível executar a autenticação durante a reprodução.

Com a rotação da licença, um ativo é criptografado com várias licenças de DRM. Cada vez que novos metadados DRM são descobertos, os métodos `DRMHelper` são usados para verificar se os metadados DRM exigem autenticação DRM.

>[!TIP]
>
>Antes de iniciar a reprodução, determine se você está lidando com uma licença vinculada ao domínio e se a autenticação do domínio é necessária. Se sim, conclua a autenticação de domínio e ingresse no domínio.

1. Quando novos Metadados DRM são descobertos em um ativo, um evento é despachado na camada do aplicativo.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
       @Override 
       public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           ... 
       } 
   };
   ```

1. Use `DRMMetadata` para verificar se a autenticação é necessária.

   * Se a autenticação não for obrigatória, você não precisará fazer nada e a reprodução continuará ininterrupta.
   * Se a autenticação for necessária, conclua a autenticação DRM.

      Como essa operação é assíncrona e é manipulada em um thread diferente, ela não afeta a interface do usuário nem a reprodução do vídeo.

1. Se a autenticação falhar, o usuário não poderá continuar a exibição do vídeo e a reprodução será interrompida.

<!--<a id="example_939B95F831A245869F9248E2767F260C"></a>-->

Por exemplo:

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo =  
          drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null ||  
          !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the  
        // current player time and the DRM metadata start time. For the time being,  
        // we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences =  
          PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
        String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
                ... 
            } 
 
            @Override 
            public void onAuthenticationError(int major,  
                                              int minor,  
                                              String erroString,  
                                              String serverErrorURL) { 
                if (getActivity() == null) { 
                    return; 
                } 
                _handler.post(new Runnable() { 
                    @Override 
                    public void run() { 
                        showToast(getString(R.string.drmAuthenticationError)); 
                        getActivity().finish(); 
                    } 
                }); 
            } 
 
            @Override 
            public void onAuthenticationComplete(byte[] authenticationToken) { 
            } 
 
        }); 
    } 
}; 
```

