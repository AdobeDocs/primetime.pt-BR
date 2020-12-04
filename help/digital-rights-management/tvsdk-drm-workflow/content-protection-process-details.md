---
seo-title: Detalhes do processo de aquisição da licença
title: Detalhes do processo de aquisição da licença
uuid: 4825c49e-fa6f-4c98-9d21-a2743930ca2e
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Detalhes do processo de aquisição de licença {#license-acquisition-process-details}

Esse processo apresenta uma visualização detalhada em nível de API do fluxo de trabalho de conteúdo protegido do DRM Primetime:

1. Usando um objeto `URLLoader`, carregue os bytes do arquivo de metadados do conteúdo protegido.

   Defina esse objeto como uma variável, como `metadata_bytes`. Todo o conteúdo controlado pelo Primetime DRM tem metadados do Primetime DRM. Quando o conteúdo é empacotado, esses metadados podem ser salvos como um arquivo de metadados separado ( [!DNL .metadata]) ao lado do conteúdo. Como alternativa, os metadados podem ser codificados em Base64 e inseridos no corpo do arquivo de manifesto do vídeo. Para obter mais informações, consulte [Empacotando arquivos de mídia](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. Se necessário, remova o ponto de exclamação `!` do start da string.
   1. Se necessário para conteúdo HLS ou HDS, decodifice os metadados incluídos na string codificada em Base64 para dados binários antes de passá-los.
1. Crie uma instância `DRMContentData`.

   Coloque este código em um bloco try-catch:

   ```
   new DRMContentData(metadata_bytes)
   ```

   em que `metadata_bytes` é o objeto `URLLoader` obtido na Etapa 1.

   [iOS: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. Crie ouvintes para acompanhar os `DRMStatusEvent` e `DRMErrorEvent` despachados do objeto `DRMManager`.

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   No listener `DRMStatusEvent`, verifique se a licença é válida (não é nula). No listener `DRMErrorEvent`, manipule `DRMErrorEvents`. Consulte *Usando a classe DRMStatusEvent* e *Usando a classe DRMErrorEvent* neste guia.

1. Carregue a licença necessária para reproduzir o conteúdo.
Primeiro, tente carregar uma licença armazenada localmente para reproduzir o conteúdo:

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android: DRMManager.acquisitionLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquisitionLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   Após a conclusão do carregamento, o objeto `DRMManager` despacha `DRMStatusEvent.DRM_Status`.

1. Verifique o objeto `DRMVoucher`.


   Se o objeto `DRMVoucher` não for nulo, a licença será válida. Vá para a Etapa 9.

   [Android: DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS: DRMLicenseAcquired](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. Verifique o método de autenticação exigido pela política para este conteúdo.

   Use a propriedade `DRMContentData.authenticationMethod`.
   1. Se o método de autenticação for `ANONYMOUS`, vá para a Etapa 9. 

      [Android: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. Se o método de autenticação for `USERNAME_AND_PASSWORD`, seu aplicativo deverá fornecer um mecanismo para permitir que o usuário insira credenciais.

      Transmita as credenciais do usuário para o servidor de licenças para autenticar o usuário:

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      O `DRMManager` despacha um `DRMAuthenticationErrorEvent` se a autenticação falhar, ou um `DRMAuthenticationCompleteEvent` se a autenticação tiver êxito. Crie ouvintes para esses eventos.

      [Android: authentication()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS: autenticar:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >A Adobe recomenda usar um mecanismo mais seguro para fornecer credenciais. Para obter referência, consulte [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. Se o método de autenticação for `UNKNOWN`, você deverá usar um método de autenticação personalizado.

      Nesse caso, o provedor de conteúdo organizou para que a autenticação seja feita de maneira fora de banda, e não usando as APIs Primetime. O procedimento de autenticação personalizado deve produzir um token de autenticação que pode ser passado para o método `DRMManager.setAuthenticationToken()`.

      [Android: setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS: setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >Como alternativa, independentemente do método de autenticação, `.setAuthenticationToken()` pode ser usado para enviar dados personalizados do cliente para o servidor de licença. Isso é uma sobrecarga da API, pois esse mecanismo é a única maneira de enviar dados personalizados dinâmicos do cliente para o servidor de licença no momento da aquisição da licença. Este método de transporte de dados personalizado é discutido em profundidade em várias postagens do fórum nos fóruns [Primetime DRM (Adobe Access) ](https://forums.adobe.com/community/adobe_access).

1. Se a autenticação falhar, seu aplicativo deverá retornar à Etapa 6.

   Certifique-se de que seu aplicativo tenha um mecanismo para manipular e limitar falhas repetidas de autenticação. Por exemplo, após três tentativas, você exibe uma mensagem para o usuário indicando que a autenticação falhou e que o conteúdo não pode ser reproduzido.
1. Para usar o token armazenado em vez de solicitar que o usuário insira credenciais, defina o token com o método `DRMManager.setAuthenticationToken()`.

   Você então baixa a licença do servidor de licença e reproduz o conteúdo como na Etapa 6.
   1. **Opcional:** se a autenticação for bem-sucedida, você poderá capturar o token de autenticação, que é uma matriz de bytes armazenada em cache na memória.

      Obtenha este token com a propriedade `DRMAuthenticationCompleteEvent.token`. Você pode armazenar e usar o token de autenticação para que o usuário não tenha que inserir credenciais repetidamente para esse conteúdo. O servidor de licenças determina o período válido do token de autenticação.

      [Android: OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS: DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. Se a autenticação tiver êxito, baixe a licença do servidor de licenças:

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   Após a conclusão do carregamento, o objeto `DRMManager` despacha `DRMStatusEvent.DRM_STATUS`. Analise este evento e, quando ele for enviado, você poderá reproduzir o conteúdo.  Reproduza o vídeo criando um objeto Primetime e chamando seu método `play()`:

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