---
description: Quando os metadados DRM de um vídeo forem incluídos no fluxo de mídia, execute a autenticação durante a reprodução.
title: Autenticação DRM durante a reprodução
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Autenticação DRM durante a reprodução {#drm-authentication-during-playback}

Quando os metadados DRM de um vídeo forem incluídos no fluxo de mídia, execute a autenticação durante a reprodução.

Considere o recurso de rotação de licença, em que um ativo é criptografado com várias licenças de DRM. Sempre que novos metadados de DRM forem detectados, use os métodos `DRMHelper` para verificar se os metadados de DRM exigem autenticação de DRM.

>[!NOTE]
>
>Este tutorial não lida com licenças vinculadas a domínios. Idealmente, antes de iniciar a reprodução, verifique se você está lidando com uma licença vinculada ao domínio. Se sim, execute a autenticação de domínio (se necessário) e participe do domínio.

1. Quando novos metadados de DRM são descobertos em um ativo, um evento é despachado na camada do aplicativo.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
           @Override 
           public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           } 
   };
   ```

1. Use o `DRMMetadata` para verificar se a autenticação é necessária. Em caso negativo, não fazer nada; a reprodução continua ininterrupta.
1. Caso contrário, execute a autenticação DRM. Como essa operação é assíncrona e é tratada em um thread diferente, não afeta a interface do usuário nem a reprodução do vídeo.
1. Se a autenticação falhar, o usuário não poderá continuar a visualização do vídeo e a reprodução será interrompida. Caso contrário, a reprodução continuará ininterruptamente.

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo = drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the current player time and the 
        // DRM metadata start time. For the time being, we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
          String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
            } 
 
            @Override 
            public void onAuthenticationError(int major, int minor, String erroString, String serverErrorURL) { 
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
