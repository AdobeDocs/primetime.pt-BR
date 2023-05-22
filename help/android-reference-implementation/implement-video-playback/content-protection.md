---
description: O reprodutor do Primetime oferece suporte à integração do Primetime DRM como fluxos de trabalho DRM personalizados. Isso significa que o aplicativo deve implementar os workflows de autenticação DRM antes de reproduzir o fluxo.
title: Proteção de conteúdo DRM
exl-id: c1904d15-023f-49fb-95f9-d157d17b3516
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Proteção de conteúdo DRM {#drm-content-protection}

O reprodutor do Primetime oferece suporte à integração do Primetime DRM como fluxos de trabalho DRM personalizados. Isso significa que o aplicativo deve implementar os workflows de autenticação DRM antes de reproduzir o fluxo.

Para ativar isso, o TVSDK fornece o gerenciador DRM para autenticação. A implementação de referência fornece um exemplo dos seguintes workflows:

* Como carregar e reproduzir fluxos HLS com proteção de acesso a conteúdo, otimizada para baixas taxas de erro e inicialização rápida.
* Como carregar e reproduzir fluxos HLS com proteção de conteúdo AES128.
* Como carregar e reproduzir fluxos HLS com proteção de conteúdo PHLS, otimizado para taxas de erro baixas e inicialização rápida.

Todo o conteúdo protegido por DRM é manipulado automaticamente pelas bibliotecas DRM integradas ao TVSDK. No entanto, você pode expor o tratamento de erros, a otimização da individualização de dispositivos e a aquisição de licença usando retornos de chamada da API TVSDK.

## Adicionar proteção de conteúdo ao reprodutor {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

Você pode adicionar proteção de conteúdo ao reprodutor criando um gerenciador de reprodução ou usando a fábrica do gerenciador.

Para criar um gerenciador de proteção de conteúdo:

* Inicialize o sistema DRM.

   O código de exemplo a seguir mostra como chamar `loadDRMServices` no aplicativo `onCreate()` para garantir que qualquer inicialização necessária para o sistema DRM seja iniciada antes do início da reprodução.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* Pré-carregar as licenças de DRM.

   O código de exemplo a seguir mostra o carregamento de `VideoItems` quando a lista de conteúdo terminar de carregar. Isso fará com que as licenças de DRM sejam adquiridas do servidor de licenças e armazenadas em cache localmente, de modo que, quando a reprodução começar, o conteúdo seja carregado com o mínimo de atraso.

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
   >Você pode definir as licenças de DRM de pré-armazenamento em cache como ATIVADAS na interface do usuário Configurações para pré-armazenar em cache as licenças de DRM ao carregar o conteúdo. No entanto, a prática recomendada é pré-carregar um item específico em vez de pré-armazenar em cache todas as licenças no catálogo.
   >
   >![](assets/precache-drm-licenses.jpg)

* Para usar `ManagerFactory` para implementar o tratamento de erros DRM, verifique se a seguinte linha de código está na [!DNL PlayerFragment.java] arquivo:

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**Documentação da API relacionada**

* [Classe DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)
