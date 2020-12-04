---
description: Você pode ativar o FairPlay para Safari ao trabalhar com a Nuvem DRM Primetime, fornecida pela ExpressPlay.
seo-description: Você pode ativar o FairPlay para Safari ao trabalhar com a Nuvem DRM Primetime, fornecida pela ExpressPlay.
seo-title: Ativar o FairPlay para Safari HLS
title: Ativar o FairPlay para Safari HLS
uuid: 6a250a31-cc4b-4c4b-b1e9-893ee3ca5d78
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Ativar o FairPlay para Safari HLS {#enable-fairplay-for-safari-hls}

Você pode ativar o FairPlay para Safari ao trabalhar com a Nuvem DRM Primetime, fornecida pela ExpressPlay.

Verifique se você tem o seguinte:

* Um aplicativo de amostra que funciona e pode reproduzir vídeo HLS.

   O aplicativo de amostra deve ser capaz de reproduzir conteúdo protegido pelo FairPlay com o licenciamento manipulado por meio do Primetime DRM com ExpressPlay.
* Amostra de conteúdo HLS (um manifesto M3U8) empacotado com proteção FairPlay.

Para usar todas as informações aqui, saiba mais sobre Workflows Multi-DRM começando com a subseção [Servidor de referência: Amostra do servidor de direito ExpressPlay (SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) no guia Workflows Multi-DRM. Primeiro, leia a documentação sobre como configurar seus direitos e o servidor de chaves, e as informações abaixo serão muito mais úteis.
Você precisa dos seguintes itens:

* Seu *autenticador de cliente* de produção do ExpressPlay
* A mesma Chave de conteúdo e `iv` com as quais o conteúdo foi empacotado.
* A localização do certificado de chave pública do FairPlay.

Para modificar seu aplicativo FairPlay / Safari:

1. Defina a localização do seu certificado de chave pública do FairPlay que foi usado na solicitação do servidor de licenças do FairPlay.

   Por exemplo:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Execute uma solicitação manual de licença do FairPlay *token* para o ExpressPlay obter um URL de token de licença.

       Você pode concluir esta etapa de uma das seguintes maneiras:
   
   * Use seu próprio Autenticador de cliente do ExpressPlay Production.
   * Use a mesma Chave de conteúdo e `iv` nesta solicitação que foram usadas para empacotar o conteúdo que deseja reproduzir.

      Execute o seguinte comando do shell e substitua seu autenticador de cliente do ExpressPlay para obter o URL do token de licença para o conteúdo de amostra:

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

   É necessário adicionar essa alteração de esquema de URL no aplicativo, antes da chamada para o servidor de licença que permite a reprodução.

   Os protocolos precisam ser alterados porque a ID do conteúdo, que fornece acesso à chave de conteúdo no sistema de gerenciamento de chaves, está empacotada no manifesto M3U8 com o protocolo `skd://`. Quando o player estiver pronto para obter a licença para reproduzir o conteúdo protegido, ele precisará primeiro alternar os protocolos para se comunicar com o servidor de licenças ExpressPlay. No exemplo abaixo, `myServerProcessSPCPath` é modificado para conter o esquema de URL correto para a solicitação do servidor de licença:

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

