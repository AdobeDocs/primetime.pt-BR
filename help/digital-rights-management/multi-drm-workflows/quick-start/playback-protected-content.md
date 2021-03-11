---
description: Para testar sua solução de DRM, você precisa de um aplicativo de vídeo que possa processar a solução de DRM específica com a qual você está trabalhando. Este reprodutor pode ser um reprodutor de amostra disponibilizado pelo Adobe ou pelo seu próprio aplicativo de vídeo baseado em TVSDK.
title: Reproduzir o conteúdo protegido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# Reproduzir o conteúdo protegido {#playback-your-protected-content}

Para testar sua solução de DRM, você precisa de um aplicativo de vídeo que possa processar a solução de DRM específica com a qual você está trabalhando. Este reprodutor pode ser um reprodutor de amostra disponibilizado pelo Adobe ou pelo seu próprio aplicativo de vídeo baseado em TVSDK.

1. Use o URL do License Server a partir da resposta do token obtida do servidor ExpressPlay para testar se você pode reproduzir seu conteúdo protegido.

   * **Widevine**  - Use a resposta Widevine diretamente, conforme recebida de sua solicitação de token de licença do ExpressPlay.
   * **PlayReady**  - Obtenha o URL do License Server e o token do objeto JSON retornados da solicitação de token de licença.
   * **FairPlay**  - Use a resposta FairPlay diretamente conforme recebido de sua solicitação de token de licença do ExpressPlay.

1. Teste a reprodução do conteúdo protegido utilizando o seu próprio player ou um player de amostra de Adobe existente.

   Forneça o URL para seu conteúdo protegido (o local do manifesto M3U8 ou MPD, dependendo de qual solução de DRM você está testando).

   Dependendo da interface fornecida pelo reprodutor com o qual você está testando, pode ser solicitado que você forneça o URL da licença e o token separadamente como cadeias de caracteres em campos de entrada, ou como um objeto JSON colado em uma caixa de texto, ou talvez como um parâmetro de consulta no URL.

   Algumas possibilidades para os players de teste estão listadas aqui:

   * Reprodutor de referência HTML5:

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * Exemplo de reprodutor TVSDK (em desenvolvimento) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **Verificar a reprodução ao testar a configuração do FairPlay:** o FairPlay requer algumas etapas adicionais para reproduzir o conteúdo quando você estiver usando os servidores de licença do ExpressPlay. Se estiver usando [!DNL curl] para testar suas conexões (conforme descrito em [Licenciamento](../../multi-drm-workflows/quick-start/handle-the-licensing.md)), será necessário *editar seu manifesto M3U8* (seu conteúdo empacotado) da seguinte maneira:

1. Adicione a resposta obtida da solicitação de token de licença à tag `#EXT-X-KEY:` no manifesto; e
1. Altere o protocolo desse URL da resposta (agora no manifesto), de `https://` para `skd://`.

   Este é um exemplo completo para testar a reprodução com o FairPlay, incluindo a etapa de licenciamento:

1. Use a solicitação de token de licença do FairPlay para obter o URL do token de licença. (Use seu próprio Autenticador de Cliente de Produção e certifique-se de usar o mesmo CEK e `iv` que foram usados para empacotar seu conteúdo do FairPlay.) Execute o seguinte comando para obter o URL do token de licença para o conteúdo de exemplo:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   Você deve obter uma resposta com o URL do token de licença que se parece com isto:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. Coloque a resposta do URL do token de licença retornado no manifesto M3U8 e *altere o esquema do URL do token de licença para* `sdk://` de `https://`. A seguir encontra-se um exemplo da tag #EXT-X-KEY no seu manifesto M3U8:

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
   >As informações anteriores se aplicam apenas ao teste de sua configuração do FairPlay. Pode não se aplicar à configuração de produção, dependendo de como você configura o manipulador do FairPlay. Consulte [Ativar o Apple FairPlay em aplicativos iOS](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) para obter detalhes.

Se o seu vídeo for reproduzido, você terá empacotado e licenciado com sucesso o seu conteúdo. Se o vídeo não for reproduzido, verifique a página de solução de problemas para encontrar soluções possíveis para os problemas.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

Por exemplo, esta é a parte da interface do usuário no primeiro reprodutor de teste listado acima, onde você fornece as informações de licenciamento obtidas do servidor ExpressPlay:

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
