---
description: O Flash Runtime TVSDK precisa de um token assinado para validar que você tem o direito de chamar a API TVSDK no domínio em que seu aplicativo está.
seo-description: O Flash Runtime TVSDK precisa de um token assinado para validar que você tem o direito de chamar a API TVSDK no domínio em que seu aplicativo está.
seo-title: Carregar o token assinado
title: Carregar o token assinado
uuid: 8760eab3-3d6d-47c6-9aa7-f64f6aa5ddcf
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Carregar o token assinado {#load-your-signed-token}

O Flash Runtime TVSDK precisa de um token assinado para validar que você tem o direito de chamar a API TVSDK no domínio em que seu aplicativo está.

1. Obtenha um token assinado de seu representante da Adobe para cada um dos domínios (onde cada domínio pode ser um domínio específico ou um domínio curinga).

       Para obter um token, forneça à Adobe o domínio em que seu aplicativo será armazenado ou carregado ou, de preferência, o domínio como um hash SHA256. Em troca, a Adobe fornece um token assinado para cada domínio. Esses tokens assumem uma destas formas:
   
   * Um [!DNL .xml] arquivo que atua como token para um domínio único ou domínio curinga.

      >[!NOTE]
      >
      >Um token para um domínio curinga abrange esse domínio e todos os seus subdomínios. Por exemplo, um token curinga para o domínio [!DNL mycompany.com] também cobriria [!DNL vids.mycompany.com] e [!DNL private.vids.mycompany.com]; um token curinga para [!DNL vids.mycompany.com] também cobriria [!DNL private.vids.mycompany.com]. *Tokens de domínio curinga são suportados apenas para determinadas versões do Flash Player.*

   * Um [!DNL .swf] arquivo contendo informações de token para vários domínios (não incluindo curingas) (único ou curinga), que seu aplicativo pode carregar dinamicamente.

1. Armazene o arquivo de token no mesmo local ou domínio que seu aplicativo.

   Por padrão, o TVSDK procura o token neste local. Como alternativa, você pode especificar o nome e o local do token `flash_vars` no arquivo HTML.
1. Se o arquivo de token for um único arquivo XML:
   1. Use `utils.AuthorizedFeaturesHelper.loadFrom` para baixar os dados armazenados no URL especificado (o arquivo de token) e extrair as `authorizedFeatures` informações dele.

      Esta etapa pode variar. Por exemplo, você pode querer executar a autenticação antes de iniciar o aplicativo ou pode receber o token diretamente do sistema de gerenciamento de conteúdo (CMS).

   1. O TVSDK despacha um `COMPLETED` evento se o carregamento for bem-sucedido ou se um `FAILED` evento for outro. Execute as ações apropriadas ao detectar qualquer um dos eventos.

      Isso deve ser bem-sucedido para que seu aplicativo forneça os `authorizedFeatures` objetos necessários ao TVSDK na forma de um `MediaPlayerContext`.
   Este exemplo mostra como você pode usar um arquivo de [!DNL .xml] token único.

   ```
   private function loadDirectTokenURL():void { 
       var url:String = constructAuthorizedFeatureTokenURL(); 
       _logger.debug("#onApplicationComplete Loading token from [{0}].", url); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE,  
           onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR,  
           onFeatureError); 
        _authorizedFeatureHelper.loadFrom(url); 
    }
   ```

1. Se o token for um [!DNL .swf] arquivo:
   1. Defina uma `Loader` classe para carregar dinamicamente o [!DNL .swf] arquivo.
   1. Defina `LoaderContext` para especificar que o carregamento esteja no domínio do aplicativo atual, o que permite que o TVSDK escolha o token correto no [!DNL .swf] arquivo. Se não `LoaderContext` for especificada, a ação padrão de `Loader.load` é carregar o .swf no domínio filho do domínio atual.
   1. Analise o evento COMPLETE, que o TVSDK despacha se a carga for bem-sucedida.

      Analise também o evento ERROR e tome as medidas apropriadas.
   1. Se a carga for bem-sucedida, use o para obter um `AuthorizedFeaturesHelper` `ByteArray` que contenha os dados de segurança codificados PCKS-7.

      Esses dados são usados por meio da API AVE V11 para obter a confirmação de autorização do Flash Runtime Player. Se a matriz de bytes não tiver conteúdo, use o procedimento para procurar um arquivo de token de domínio único.
   1. Use `AuthorizedFeatureHelper.loadFeatureFromData` para obter os dados necessários da matriz de bytes.
   1. Descarregue o [!DNL .swf] arquivo.
   Os exemplos a seguir mostram como você pode usar um arquivo de vários token [!DNL .swf] .

   **Exemplo 1 de vários token:**

   ```
   private function onApplicationComplete(event:FlexEvent):void { 
       var url:String = constructAuthorizedFeatureTokenURLFromSwf();   
       _loader = new Loader(); 
       var swfUrl:URLRequest = new URLRequest(url); 
       var loaderContext:LoaderContext =  
           new LoaderContext(false, ApplicationDomain.currentDomain, null); 
       _loader.contentLoaderInfo.addEventListener(Event.COMPLETE,  
           modEventHandler); 
       _loader.contentLoaderInfo.addEventListener(IOErrorEvent.IO_ERROR,  
           errEventHandler); 
       _loader.contentLoaderInfo.addEventListener(ProgressEvent.PROGRESS,  
           onProgressHandler); 
       _loader.uncaughtErrorEvents.addEventListener(UncaughtErrorEvent. 
           UNCAUGHT_ERROR, uncaughtEventHandler); 
       _logger.debug("# Loading token swf with context from [{0}].", url); 
       _loader.load(swfUrl, loaderContext); 
   } 
   
   private function modEventHandler(e:Event):void { 
       _logger.debug("loadSWF with domainID {0}",  
       SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
           loader.contentLoaderInfo.applicationDomain. 
           getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray = myTokens. 
           FetchToken(SecurityDomain.currentDomain.domainID); 
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           _logger.debug("token bytearry size {0}", byteArray.length); 
           _authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   ```

   **Exemplo 2 de vários token:**

   ```
   private function tokenSwfLoadedHandler(e:Event):void { 
       trace("loadSWF with domainID {0}", SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
         loader.contentLoaderInfo.applicationDomain. 
         getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray =  
           myTokens.FetchToken(SecurityDomain.currentDomain.domainID); 
       var myDomains:Array = ["domain.com"]; 
       if (byteArray == null || byteArray.length == 0) { 
           // check for wildcard tokens 
           if (myTokens.hasOwnProperty("FetchWildCardToken") == true) { 
               // contains wildcard domains 
               for each (var domain:String in myDomains) { 
                   byteArray = myTokens.FetchWildCardToken(domain); 
                   if (byteArray != null && byteArray.length != 0) { 
                       break; 
                   } 
               }; 
           } 
       } 
   
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           trace("token bytearry size {0}", byteArray.length); 
           authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   
   private function loadDirectTokenURL():void { 
       trace("#onApplicationComplete Loading token from [{0}].", tokenUrl); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       authorizedFeatureHelper.loadFrom(tokenUrl); 
   }
   ```

