---
description: Você pode ativar o FairPlay para Safari ao trabalhar com a Nuvem DRM do Primetime, ativada pelo ExpressPlay.
title: Ativar FairPlay para Safari HLS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Ativar FairPlay para Safari HLS {#enable-fairplay-for-safari-hls}

Você pode ativar o FairPlay para Safari ao trabalhar com a Nuvem DRM do Primetime, ativada pelo ExpressPlay.

Certifique-se de ter o seguinte:

* Um aplicativo de amostra funcional que pode reproduzir vídeo HLS.

  O aplicativo de amostra deve ser capaz de reproduzir conteúdo protegido por FairPlay com o licenciamento manipulado pelo DRM do Primetime viabilizado pelo ExpressPlay.
* Exemplo de conteúdo HLS (um manifesto M3U8) empacotado com proteção FairPlay.

Para usar todas as informações aqui, saiba mais sobre os fluxos de trabalho de vários DRMs começando com a subseção [Servidor de Referência: Exemplo de Servidor de Direitos ExpressPlay (SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) no guia Fluxos de trabalho de vários DRM. Leia primeiro essa documentação sobre como configurar seu servidor de direitos e chaves, e as informações abaixo serão muito mais úteis.
Você precisa dos seguintes itens:

* Seu *produção* Autenticador do cliente da ExpressPlay
* A mesma chave de conteúdo e `iv` com o qual seu conteúdo foi empacotado.
* O local do certificado de chave pública FairPlay.

Para modificar o aplicativo FairPlay/Safari:

1. Defina o local do certificado de chave pública FairPlay usado na solicitação do servidor de licença FairPlay.

   Por exemplo:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Executar uma licença FairPlay manual *token* solicitação ao ExpressPlay para obter um URL do token de licença.

       Você pode concluir essa etapa de uma das seguintes maneiras:
   
   * Use seu próprio Autenticador de Cliente de Produção ExpressPlay.
   * Usar a mesma Chave de conteúdo e `iv` nesta solicitação, que foi usada para empacotar o conteúdo que você deseja reproduzir.

     Execute o seguinte comando no shell e substitua seu autenticador de cliente ExpressPlay para obter o URL do token de licença para o conteúdo de amostra:

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

1. Antes que seu aplicativo possa reproduzir um conteúdo protegido, altere o esquema de URL do conteúdo de `skd://` para `https://`.

   É necessário adicionar essa alteração de esquema de URL no aplicativo antes da chamada para o servidor de licença que permite a reprodução.

   Os protocolos precisam ser alterados porque a ID de Conteúdo, que fornece acesso à Chave de Conteúdo no Sistema de Gerenciamento de Chaves, está empacotada no manifesto M3U8 com a variável `skd://` protocolo. Quando o reprodutor estiver pronto para obter a licença para reproduzir o conteúdo protegido, ele precisará primeiro alternar os protocolos para se comunicar com o servidor de licenças ExpressPlay. No exemplo abaixo, a variável `myServerProcessSPCPath` foi modificado para conter o esquema de URL correto para a solicitação do servidor de licença:

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
