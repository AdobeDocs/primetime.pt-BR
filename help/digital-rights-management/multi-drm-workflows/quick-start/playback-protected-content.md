---
description: Para testar sua solução DRM, é necessário um aplicativo de vídeo que possa processar a solução DRM específica com a qual você está trabalhando. Este player pode ser um player de amostra disponibilizado pelo Adobe ou seu próprio aplicativo de vídeo baseado em TVSDK.
seo-description: Para testar sua solução DRM, é necessário um aplicativo de vídeo que possa processar a solução DRM específica com a qual você está trabalhando. Este player pode ser um player de amostra disponibilizado pelo Adobe ou seu próprio aplicativo de vídeo baseado em TVSDK.
seo-title: Reproduzir o conteúdo protegido
title: Reproduzir o conteúdo protegido
uuid: 84f73ee7-43d0-481c-a5e7-14f92169323c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# Reproduzir o conteúdo protegido {#playback-your-protected-content}

Para testar sua solução DRM, é necessário um aplicativo de vídeo que possa processar a solução DRM específica com a qual você está trabalhando. Este player pode ser um player de amostra disponibilizado pelo Adobe ou seu próprio aplicativo de vídeo baseado em TVSDK.

1. Use o URL do License Server na resposta do token que você obteve do servidor ExpressPlay para testar se você pode reproduzir seu conteúdo protegido.

   * **Widevine** - Use a resposta do Widevine diretamente conforme recebido de sua solicitação de token de licença do ExpressPlay.
   * **PlayReady** - Obtenha o URL e o token do servidor de licença do objeto JSON retornado da solicitação de token de licença.
   * **FairPlay** - Use a resposta do FairPlay diretamente como recebido de sua solicitação de token de licença do ExpressPlay.

1. Teste a reprodução de seu conteúdo protegido utilizando seu próprio player ou um player de amostra de Adobe existente.

   Forneça o URL para seu conteúdo protegido (o local do seu manifesto M3U8 ou MPD, dependendo da solução DRM que você estiver testando).

   Dependendo da interface fornecida pelo player com o qual você está testando, pode ser solicitado que você forneça o URL da licença e o token separadamente como strings nos campos de entrada, ou como um objeto JSON colado em uma caixa de texto, ou talvez como um parâmetro de query no URL.

   Algumas possibilidades para os players de teste estão listadas aqui:

   * Reprodutor de referência HTML5:

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * Amostra do TVSDK Player (em desenvolvimento) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **Verificar a reprodução ao testar a configuração do FairPlay:** O FairPlay requer algumas etapas adicionais para reproduzir o conteúdo quando você estiver usando os servidores de licença do ExpressPlay. Se você estiver usando [!DNL curl] para testar suas conexões (conforme descrito em [Licenciamento](../../multi-drm-workflows/quick-start/handle-the-licensing.md)), é necessário *editar seu manifesto* M3U8 (seu conteúdo empacotado) da seguinte maneira:

1. Adicione a resposta que você obteve de volta da solicitação de token de licença à `#EXT-X-KEY:` tag do manifesto; e
1. Altere o protocolo desse URL da resposta (agora no manifesto), de `https://` para `skd://`.

   Este é um exemplo completo para testar a reprodução com o FairPlay, incluindo a etapa de licenciamento:

1. Use a solicitação de token de licença do FairPlay para obter o URL do token de licença. (Use seu próprio Autenticador de cliente de produção e certifique-se de usar o mesmo CEK e `iv` que foi usado para disponibilizar seu conteúdo do FairPlay.) Execute o seguinte comando para obter o URL do token de licença para o conteúdo de exemplo:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   Você deve obter uma resposta com o URL do token de licença que se parece com isso:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. Coloque a resposta do URL do token de licença retornado no manifesto M3U8 e *altere o esquema do URL do token de licença para* `sdk://` de `https://`. Veja a seguir um exemplo da tag #EXT-X-KEY no seu manifesto M3U8:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES, 
   URI="skd://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g- 
   CR1rnJKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPx 
   N5qomYsnwYSSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw", 
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1"
   ```

   >[!NOTE]
   >
   >As informações anteriores se aplicam somente ao teste da configuração do FairPlay. Pode não se aplicar à configuração de produção, dependendo de como você configura o seu manipulador do FairPlay. Consulte [Ativar o Apple FairPlay em aplicativos](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) iOS para obter detalhes.

Se o vídeo for reproduzido, você empacotou e licenciou com êxito o conteúdo. Se o vídeo não for reproduzido, verifique na página de solução de problemas se há possíveis soluções para os problemas.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

Por exemplo, esta é a parte da interface do usuário no primeiro player de teste listado acima, onde você fornece as informações de licenciamento obtidas do servidor ExpressPlay:

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
