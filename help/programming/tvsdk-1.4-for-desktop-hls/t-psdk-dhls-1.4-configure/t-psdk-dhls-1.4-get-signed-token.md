---
description: O TVSDK do Flash Runtime precisa de um token assinado para validar se você tem o direito de chamar a API TVSDK no domínio em que o aplicativo reside.
title: Carregar seu token assinado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Carregar seu token assinado {#load-your-signed-token}

O TVSDK do Flash Runtime precisa de um token assinado para validar se você tem o direito de chamar a API TVSDK no domínio em que o aplicativo reside.

1. Obtenha um token assinado do representante da Adobe para cada um dos domínios (em que cada domínio pode ser um domínio específico ou um domínio curinga).

       Para obter um token, forneça ao Adobe o domínio em que seu aplicativo será armazenado ou carregado ou, preferencialmente, o domínio como um hash SHA256. Em troca, o Adobe fornece um token assinado para cada domínio. Esses tokens assumem uma destas formas:
   
   * Um [!DNL .xml] arquivo que atua como token para um único domínio ou domínio curinga.

     >[!NOTE]
     >
     >Um token para um domínio curinga abrange esse domínio e todos os seus subdomínios. Por exemplo, um token curinga para o domínio [!DNL mycompany.com] abrangerá igualmente [!DNL vids.mycompany.com] e [!DNL private.vids.mycompany.com]; um token curinga para [!DNL vids.mycompany.com] abrangerá igualmente [!DNL private.vids.mycompany.com]. *Os tokens de domínio curinga são compatíveis somente com determinadas versões do Flash Player.*

   * A [!DNL .swf] arquivo que contém informações de token para vários domínios (sem incluir curingas) (único ou curinga), que seu aplicativo pode carregar dinamicamente.

1. Armazene o arquivo de token no mesmo local ou domínio do aplicativo.

   Por padrão, o TVSDK procura o token neste local. Como alternativa, você pode especificar o nome e o local do token em `flash_vars` no arquivo HTML.
1. Se o arquivo de token for um único arquivo XML:
   1. Uso `utils.AuthorizedFeaturesHelper.loadFrom` para baixar os dados armazenados no URL especificado (o arquivo de token) e extrair o `authorizedFeatures` suas informações.

      Esta etapa pode variar. Por exemplo, talvez você queira executar a autenticação antes de iniciar o aplicativo ou pode receber o token diretamente do seu sistema de gerenciamento de conteúdo (CMS).

   1. O TVSDK despacha um `COMPLETED` evento se a carga for bem-sucedida ou um `FAILED` caso contrário. Execute a ação apropriada ao detectar qualquer um dos eventos.

      Isso deve ser bem-sucedido para que seu aplicativo forneça os `authorizedFeatures` objetos para o TVSDK na forma de um `MediaPlayerContext`.

   Este exemplo mostra como é possível usar um token único [!DNL .xml] arquivo.

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
   1. Definir um `Loader` para carregar dinamicamente a [!DNL .swf] arquivo.
   1. Defina o `LoaderContext` para especificar o carregamento a ser feito no domínio de aplicativo atual, o que permite ao TVSDK escolher o token correto no [!DNL .swf] arquivo. Se `LoaderContext` não for especificada, a ação padrão de `Loader.load` é para carregar o .swf no domínio filho do domínio atual.
   1. Analise o evento COMPLETE, que o TVSDK despachará se a carga for bem-sucedida.

      Além disso, acompanhe o evento ERROR e tome as medidas adequadas.
   1. Se a carga for bem-sucedida, use o `AuthorizedFeaturesHelper` para obter um `ByteArray` que contém os dados de segurança codificados por PCKS-7.

      Esses dados são usados por meio da API do AVE V11 para obter a confirmação de autorização do reprodutor do tempo de execução do Flash. Se a matriz de bytes não tiver conteúdo, use o procedimento para procurar um arquivo de token de domínio único.
   1. Uso `AuthorizedFeatureHelper.loadFeatureFromData` para obter os dados necessários da matriz de bytes.
   1. Descarregue o [!DNL .swf] arquivo.

   Os exemplos a seguir mostram como é possível usar uma interface de vários tokens [!DNL .swf] arquivo.

   **Exemplo 1 de vários tokens:**

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

   **Exemplo 2 de vários tokens:**

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
