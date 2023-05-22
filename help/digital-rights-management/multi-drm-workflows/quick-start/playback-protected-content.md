---
description: Para testar sua solução de DRM, você precisa de um aplicativo de vídeo que possa processar a solução de DRM específica com a qual você está trabalhando. Esse player pode ser um player de amostra disponibilizado pelo Adobe ou por seu próprio aplicativo de vídeo baseado em TVSDK.
title: Reproduzir seu conteúdo protegido
exl-id: b0e09474-f752-495f-a702-93f288535403
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Reproduzir seu conteúdo protegido {#playback-your-protected-content}

Para testar sua solução de DRM, você precisa de um aplicativo de vídeo que possa processar a solução de DRM específica com a qual você está trabalhando. Esse player pode ser um player de amostra disponibilizado pelo Adobe ou por seu próprio aplicativo de vídeo baseado em TVSDK.

1. Use o URL do License Server na resposta do token que você recebeu do servidor ExpressPlay para testar se é possível reproduzir seu conteúdo protegido.

   * **Widevine** - Use a resposta do Widevine diretamente conforme recebida de sua solicitação de token de licença ExpressPlay.
   * **PlayReady** - Obtenha o URL e o token do License Server do objeto JSON retornado da solicitação de token de licença.
   * **FairPlay** - Use a resposta FairPlay diretamente como recebida de sua solicitação de token de licença ExpressPlay.

1. Teste a reprodução do seu conteúdo protegido utilizando o seu próprio player ou um player de amostra Adobe existente.

   Forneça o URL para o conteúdo protegido (o local do manifesto M3U8 ou MPD, dependendo da solução de DRM que você está testando).

   Dependendo da interface fornecida pelo reprodutor com o qual você testa, talvez seja solicitado que você forneça o URL de licença e o token separados como cadeias de caracteres em campos de entrada ou como um objeto JSON colado em uma caixa de texto ou talvez como um parâmetro de consulta no URL.

   Algumas possibilidades para reprodutores de teste estão listadas aqui:

   * Reprodutor de referência HTML5:

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * Reprodutor TVSDK de exemplo (em desenvolvimento) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **Verificação da reprodução ao testar a configuração do FairPlay:** O FairPlay requer algumas etapas adicionais para reproduzir o conteúdo quando você está usando os servidores de licença ExpressPlay. Se você estiver usando [!DNL curl] para testar suas conexões (conforme descrito em [Licenciamento](../../multi-drm-workflows/quick-start/handle-the-licensing.md)), é necessário *editar o manifesto M3U8* (seu conteúdo empacotado) da seguinte maneira:

1. Adicione a resposta que você recebeu da solicitação de token de licença à `#EXT-X-KEY:` no manifesto; e
1. Altere o protocolo desse URL da resposta (agora no manifesto), de `https://` para `skd://`.

   Este é um exemplo completo para testar a reprodução com o FairPlay, incluindo a etapa de licenciamento:

1. Use a solicitação de token de licença do FairPlay para obter o URL do token de licença. (Use seu próprio Autenticador de produção do cliente e certifique-se de usar o mesmo CEK e `iv` que foi usado para empacotar seu conteúdo FairPlay.) Execute o seguinte comando para obter o URL do token de licença para o conteúdo de exemplo:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   Você deve obter uma resposta com o URL do token de licença semelhante a:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. Coloque a resposta do URL do token de licença retornado no manifesto M3U8 e *alterar o esquema do URL do token de licença para* `sdk://` de `https://`. Veja a seguir um exemplo da tag #EXT-X-KEY no manifesto M3U8:

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
   >As informações anteriores se aplicam apenas ao teste da configuração do FairPlay. Isso pode não se aplicar à configuração de produção, dependendo de como você configura o manipulador FairPlay. Consulte [Ativar o Apple FairPlay nos aplicativos do iOS](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) para obter detalhes.

Se o vídeo for reproduzido, você empacotou e licenciou o conteúdo com êxito. Se o vídeo não for reproduzido, consulte a página de solução de problemas para obter algumas soluções possíveis para os seus problemas.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

Por exemplo, esta é a parte da interface do usuário no primeiro player de teste listado acima, onde você fornece as informações de licenciamento obtidas do servidor ExpressPlay:

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
