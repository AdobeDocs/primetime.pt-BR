---
title: Detalhes do processo de aquisição da licença
description: Detalhes do processo de aquisição da licença
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Detalhes do processo de aquisição de licença {#license-acquisition-process-details}

Esse processo apresenta uma visualização detalhada em nível de API do fluxo de trabalho de conteúdo protegido do DRM do Primetime:

1. Usando um objeto `URLLoader`, carregue os bytes do arquivo de metadados do conteúdo protegido.

   Defina esse objeto como uma variável, como `metadata_bytes`. Todo o conteúdo controlado pelo DRM do Primetime tem metadados de DRM do Primetime. Quando o conteúdo é empacotado, esses metadados podem ser salvos como um arquivo de metadados separado ( [!DNL .metadata]) ao lado do conteúdo. Como alternativa, os metadados podem ser codificados em Base64 e inseridos no corpo do arquivo de manifesto do vídeo. Para obter mais informações, consulte [Empacotando arquivos de mídia](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. Se necessário, remova o ponto de exclamação `!` do início da string.
   1. Se necessário para o conteúdo HLS ou HDS, decodifice os metadados incluídos na string codificada em Base64 para dados binários antes de passá-los.
1. Crie uma instância `DRMContentData`.

   Coloque este código em um bloco try-catch:

   ```
   new DRMContentData(metadata_bytes)
   ```

   onde `metadata_bytes` é o objeto `URLLoader` obtido na Etapa 1.

   [iOS: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. Crie ouvintes para ouvir o `DRMStatusEvent` e `DRMErrorEvent` despachados do objeto `DRMManager`.

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   No ouvinte `DRMStatusEvent`, verifique se a licença é válida (não nula). No ouvinte `DRMErrorEvent`, manipule `DRMErrorEvents`. Consulte *Uso da classe DRMStatusEvent* e *Uso da classe DRMErrorEvent* neste guia.

1. Carregue a licença necessária para reproduzir o conteúdo.
Primeiro, tente carregar uma licença armazenada localmente para reproduzir o conteúdo:

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android: DRMManager.acquisitionLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquisitionLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   Depois que o carregamento é concluído, o objeto `DRMManager` despacha `DRMStatusEvent.DRM_Status`.

1. Verifique o objeto `DRMVoucher`.


   Se o objeto `DRMVoucher` não for nulo, a licença será válida. Vá para a Etapa 9.

   [Android: DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS: DRMLicenseAcquired](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. Verifique o método de autenticação exigido pela política para esse conteúdo.

   Use a propriedade `DRMContentData.authenticationMethod` .
   1. Se o método de autenticação for `ANONYMOUS`, vá para a Etapa 9. 

      [Android: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. Se o método de autenticação for `USERNAME_AND_PASSWORD`, o aplicativo deverá fornecer um mecanismo para permitir que o usuário insira credenciais.

      Passe as credenciais do usuário para o servidor de licenças para autenticar o usuário:

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      O `DRMManager` despacha um `DRMAuthenticationErrorEvent` se a autenticação falhar ou um `DRMAuthenticationCompleteEvent` se a autenticação for bem-sucedida. Crie ouvintes para esses eventos.

      [Android: authentication()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS: autenticar:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >A Adobe recomenda usar um mecanismo mais seguro para fornecer credenciais. Para referência, consulte [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. Se o método de autenticação for `UNKNOWN`, você deverá usar um método de autenticação personalizado.

      Nesse caso, o provedor de conteúdo organizou a autenticação para ser feita de maneira out-of-band, não usando as APIs do Primetime. O procedimento de autenticação personalizado deve produzir um token de autenticação que pode ser passado para o método `DRMManager.setAuthenticationToken()`.

      [Android: setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS: setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >Como alternativa, independentemente do método de autenticação, `.setAuthenticationToken()` pode ser usado para enviar dados personalizados do cliente para o servidor de licença. Isso é uma sobrecarga da API, pois esse mecanismo é a única maneira de enviar dados personalizados dinâmicos do cliente para o servidor de licença no momento da aquisição da licença. Esse método de transporte de dados personalizado é detalhado em várias publicações do fórum nos fóruns [DRM (Adobe Access) do Primetime ](https://forums.adobe.com/community/adobe_access).

1. Se a autenticação falhar, seu aplicativo deverá retornar para a Etapa 6.

   Certifique-se de que o aplicativo tenha um mecanismo para lidar com e limitar falhas de autenticação repetidas. Por exemplo, após três tentativas, você exibe uma mensagem ao usuário indicando que a autenticação falhou e o conteúdo não pode ser reproduzido.
1. Para usar o token armazenado, em vez de solicitar que o usuário insira credenciais, defina o token com o método `DRMManager.setAuthenticationToken()`.

   Em seguida, baixe a licença do servidor de licença e reproduza o conteúdo como na Etapa 6.
   1. **Opcional:** se a autenticação for bem-sucedida, você poderá capturar o token de autenticação, que é uma matriz de bytes armazenada em cache na memória.

      Obtenha esse token com a propriedade `DRMAuthenticationCompleteEvent.token`. Você pode armazenar e usar o token de autenticação para que o usuário não precise inserir credenciais repetidamente para esse conteúdo. O servidor de licenças determina o período válido do token de autenticação.

      [Android: OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS: DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. Se a autenticação tiver êxito, baixe a licença do servidor de licença:

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   Depois que o carregamento é concluído, o objeto `DRMManager` despacha `DRMStatusEvent.DRM_STATUS`. Analise esse evento e, quando ele for enviado, você poderá reproduzir o conteúdo.  Reproduza o vídeo criando um objeto Primetime e, em seguida, chamando seu método `play()`:

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android: acquisitionLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquisitionLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)