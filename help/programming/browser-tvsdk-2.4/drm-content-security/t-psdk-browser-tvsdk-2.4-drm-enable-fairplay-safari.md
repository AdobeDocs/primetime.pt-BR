---
description: Você pode ativar o FairPlay para Safari ao trabalhar com a Nuvem de DRM do Primetime, fornecida pelo ExpressPlay.
title: Ativar o FairPlay para Safari HLS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Ativar o FairPlay para Safari HLS {#enable-fairplay-for-safari-hls}

Você pode ativar o FairPlay para Safari ao trabalhar com a Nuvem de DRM do Primetime, fornecida pelo ExpressPlay.

Certifique-se de ter o seguinte:

* Um aplicativo de amostra funcional que pode reproduzir vídeo HLS.

   O aplicativo de amostra deve ser capaz de reproduzir conteúdo protegido pelo FairPlay com o licenciamento manipulado por meio do Primetime DRM fornecido pela ExpressPlay.
* Amostra de conteúdo HLS (um manifesto M3U8) empacotado com proteção FairPlay.

Para utilizar todas as informações aqui, saiba mais sobre fluxos de trabalho de vários DRM, começando pela subseção [Servidor de referência: Exemplo de SEES (ExpressPlay Entitlement Server)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) no guia de workflows de vários DRM. Primeiro leia essa documentação sobre como configurar seu direito e servidor de chaves, e as informações abaixo serão muito mais úteis.
Você precisa dos seguintes itens:

* Seu *Autenticador de cliente de produção* do ExpressPlay
* A mesma Chave de conteúdo e `iv` com as quais o conteúdo foi empacotado.
* A localização do seu certificado de chave pública do FairPlay.

Para modificar o aplicativo FairPlay / Safari:

1. Defina a localização do seu certificado de chave pública do FairPlay que foi usado na solicitação do servidor de licenças do FairPlay.

   Por exemplo:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Execute uma solicitação manual de licença do FairPlay *token* para o ExpressPlay obter um URL de token de licença.

       Você pode concluir essa etapa de uma das seguintes maneiras:
   
   * Use seu próprio Autenticador de cliente de produção ExpressPlay.
   * Use a mesma Chave de conteúdo e `iv` nesta solicitação que foi usada para empacotar o conteúdo que deseja reproduzir.

      Execute o seguinte comando do shell e substitua o autenticador de cliente do ExpressPlay para obter o URL do token de licença para o conteúdo de amostra:

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      A resposta com o URL do token de licença será semelhante a:

      ```
      https://fp.service.expressplay.com:80/hms/fp/rights/? 
           ExpressPlayToken=<base64-encoded ExpressPlay token>
      ```

1. Defina uma variável com o URL do token de licença do ExpressPlay.

   Por exemplo:

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. Antes que seu aplicativo possa reproduzir conteúdo protegido, altere o esquema de URL para o conteúdo de `skd://` para `https://`.

   Você precisa adicionar essa alteração no esquema de URL do seu aplicativo, antes da chamada para o servidor de licença que permite a reprodução.

   Os protocolos precisam ser alterados, pois a ID do conteúdo, que fornece acesso à Chave de conteúdo no Sistema de gerenciamento de chaves, é empacotada no manifesto M3U8 com o protocolo `skd://`. Quando o reprodutor está pronto para obter a licença para reproduzir o conteúdo protegido, ele precisa primeiro mudar os protocolos para se comunicar com o servidor de licenças ExpressPlay. No exemplo abaixo, `myServerProcessSPCPath` é modificado para conter o esquema de URL correto para a solicitação do servidor de licença:

   ```js
   extractContentId(initData) {  
       contentId = arrayToString(initData); // contentId is passed up as a URI,  
                                            // from which the host must be extracted:  
       var link = document.createElement('a');  
       link.href = contentId;  
       var index = contentId.indexOf(':');  
       myServerProcessSPCPath = "https:" + contentId.substring(index+1);  
       console.log("severProcessSPCPAth = " + serverProcessSPCPath); return link.hostname;  
   }
   ```

