---
description: O player do Primetime oferece suporte à integração de DRM do Primetime como fluxos de trabalho de DRM personalizados. Isso significa que o aplicativo deve implementar os workflows de autenticação de DRM antes de reproduzir o fluxo.
title: Proteção de conteúdo DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Proteção de conteúdo DRM {#drm-content-protection}

O player do Primetime oferece suporte à integração de DRM do Primetime como fluxos de trabalho de DRM personalizados. Isso significa que o aplicativo deve implementar os workflows de autenticação de DRM antes de reproduzir o fluxo.

Para habilitar isso, o TVSDK fornece o gerenciador de DRM para autenticação. A implementação de referência fornece um exemplo dos seguintes fluxos de trabalho:

* Como carregar e reproduzir fluxos HLS com proteção de conteúdo de acesso, otimizada para baixas taxas de erro e inicialização rápida.
* Como carregar e reproduzir fluxos HLS com proteção de conteúdo AES128.
* Como carregar e reproduzir fluxos HLS com proteção de conteúdo PHLS, otimizado para baixas taxas de erro e inicialização rápida.

Todo o conteúdo protegido por DRM é manipulado automaticamente pelas bibliotecas de DRM integradas ao TVSDK. No entanto, você pode expor o tratamento de erros, a otimização da individualização de dispositivos e a aquisição de licenças usando retornos de chamada da API TVSDK.

## Adicionar proteção de conteúdo ao reprodutor {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

Você pode adicionar proteção de conteúdo ao reprodutor criando um gerenciador de reprodução ou usando a fábrica do gerenciador.

Para criar um gerenciador de proteção de conteúdo:

* Inicialize o sistema DRM.

   O exemplo de código a seguir mostra a chamada de `loadDRMServices` na função `onCreate()` do aplicativo, para garantir que qualquer inicialização necessária para o sistema DRM seja iniciada antes do início da reprodução.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* Pré-carregue as licenças de DRM.

   O exemplo de código a seguir mostra como carregar o `VideoItems` quando a lista de conteúdo terminou de ser carregada. Isso resultará na aquisição das licenças de DRM no servidor de licença e no armazenamento em cache localmente, de modo que, quando a reprodução começar, o conteúdo será carregado com o mínimo de atraso.

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
   >Você pode definir licenças de DRM do Precache como ON na interface do usuário de Configurações para pré-carregar as licenças de DRM ao carregar conteúdo. No entanto, a prática recomendada é pré-carregar um item específico em vez de pré-carregar todas as licenças no catálogo.
   >
   >![](assets/precache-drm-licenses.jpg)

* Para usar `ManagerFactory` para implementar o tratamento de erros de DRM, verifique se a seguinte linha de código está no arquivo [!DNL PlayerFragment.java]:

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**Documentação da API relacionada**

* [Classe DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)