---
description: Quando os metadados de DRM de um vídeo forem incluídos no fluxo de mídia, execute a autenticação durante a reprodução.
title: Autenticação DRM durante a reprodução
exl-id: 3f190d37-291e-4a5e-811d-7e9984a6a44a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Autenticação DRM durante a reprodução {#drm-authentication-during-playback}

Quando os metadados de DRM de um vídeo forem incluídos no fluxo de mídia, execute a autenticação durante a reprodução.

Considere o recurso de rotação de licença, em que um ativo é criptografado com várias licenças DRM. Sempre que novos metadados de DRM forem descobertos, use `DRMHelper` métodos para verificar se os metadados de DRM exigem autenticação DRM.

>[!NOTE]
>
>Este tutorial não lida com licenças vinculadas ao domínio. Idealmente, antes de iniciar a reprodução, verifique se você está lidando com uma licença vinculada a um domínio. Em caso afirmativo, execute a autenticação de domínio (se necessário) e ingresse no domínio.

1. Quando novos Metadados de DRM são descobertos em um ativo, um evento é despachado na camada do aplicativo.

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

1. Use o `DRMMetadata` para verificar se a autenticação é necessária. Caso contrário, não faça nada; a reprodução continua ininterrupta.
1. Caso contrário, execute a autenticação DRM. Como essa operação é assíncrona e é manipulada em um thread diferente, ela não tem impacto na interface do usuário nem na reprodução de vídeo.
1. Se a autenticação falhar, o usuário não poderá continuar visualizando o vídeo e a reprodução será interrompida. Caso contrário, a reprodução continuará ininterruptamente.

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
