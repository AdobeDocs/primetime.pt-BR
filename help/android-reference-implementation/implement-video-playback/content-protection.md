---
description: O player Primetime oferece suporte à integração do Primetime DRM como fluxos de trabalho personalizados de DRM. Isso significa que seu aplicativo deve implementar os fluxos de trabalho de autenticação DRM antes de reproduzir o fluxo.
seo-description: O player Primetime oferece suporte à integração do Primetime DRM como fluxos de trabalho personalizados de DRM. Isso significa que seu aplicativo deve implementar os fluxos de trabalho de autenticação DRM antes de reproduzir o fluxo.
seo-title: Proteção de conteúdo DRM
title: Proteção de conteúdo DRM
uuid: 95c446f6-8304-4d70-9bef-7368b9364025
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Proteção de conteúdo DRM {#drm-content-protection}

O player Primetime oferece suporte à integração do Primetime DRM como fluxos de trabalho personalizados de DRM. Isso significa que seu aplicativo deve implementar os fluxos de trabalho de autenticação DRM antes de reproduzir o fluxo.

Para habilitar isso, o TVSDK fornece o gerenciador de DRM para autenticação. A implementação de referência fornece um exemplo dos seguintes fluxos de trabalho:

* Como carregar e reproduzir fluxos HLS com proteção de conteúdo do Access, otimizado para taxas de erro baixas e inicialização rápida.
* Como carregar e reproduzir fluxos HLS com proteção de conteúdo AES128.
* Como carregar e reproduzir fluxos HLS com proteção de conteúdo PHLS, otimizado para taxas de erro baixas e inicialização rápida.

Todo o conteúdo protegido por DRM é manipulado automaticamente pelas bibliotecas DRM incorporadas ao TVSDK. Entretanto, é possível expor a manipulação de erros, a otimização da individualização de dispositivos e a aquisição de licenças usando retornos de chamada da API TVSDK.

## Adicionar proteção de conteúdo ao player {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

Você pode adicionar proteção de conteúdo ao player criando um gerenciador de reprodução ou usando a fábrica do gerenciador.

Para criar um gerenciador de proteção de conteúdo:

* Inicialize o sistema DRM.

   O exemplo de código a seguir mostra a chamada `loadDRMServices` na `onCreate()` função do aplicativo, para garantir que qualquer inicialização necessária para o sistema DRM seja iniciada antes do início da reprodução.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* Pré-carregar as licenças de DRM.

   O exemplo de código a seguir mostra como carregar o `VideoItems` quando a lista de conteúdo terminar de carregar. Isso resultará na aquisição de licenças DRM do servidor de licenças e no cache local, de modo que, quando a reprodução for iniciada, o conteúdo será carregado com um atraso mínimo.

   ```java
   DrmManager.preLoadDrmLicenses(item.getUrl(),  
     new MediaPlayerItemLoader.LoaderListener() { 
   
       @Override 
       public void onLoadComplete(MediaPlayerItem item) { 
           Player.logger.w(LOG_TAG + "::DRMPreload#onLoadComplete", item.getResource().getUrl()); 
       } 
   
       @Override 
       public void onError(MediaErrorCode errorCode, String s) { 
           Player.logger.e(LOG_TAG + "::DRMPreload#onError", s); 
       } 
   } 
   ```

   >[!NOTE]
   >
   >Você pode definir licenças de DRM com precisão como ON na interface do usuário de Configurações para pré-armazenar as licenças de DRM ao carregar o conteúdo. No entanto, a prática recomendada é pré-carregar um item específico em vez de pré-carregar todas as licenças no catálogo.
   >
   >![](assets/precache-drm-licenses.jpg)

* Para usar `ManagerFactory` para implementar a manipulação de erros do DRM, verifique se a seguinte linha de código está no [!DNL PlayerFragment.java] arquivo:

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**Documentação da API relacionada**

* [Classe DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)