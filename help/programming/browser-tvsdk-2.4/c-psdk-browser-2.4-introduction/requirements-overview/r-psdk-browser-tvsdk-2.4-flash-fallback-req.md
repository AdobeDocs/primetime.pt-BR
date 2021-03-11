---
description: Para usar o Flash Player, verifique se o ambiente atende aos requisitos necessários.
title: Requisitos do Flash Player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---


# Requisitos do Flash Player{#flash-player-requirements}

Para usar o Flash Player, verifique se o ambiente atende aos requisitos necessários.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Estes são os requisitos para o Flash Player:

* Para reproduzir com `Primetime.js`, instale pelo menos a versão 23 do Flash Player.
* Para ser solicitado a fornecer atualizações para o Flash Player versão 23 ou posterior, instale pelo menos o Flash Player versão 11.0.0.

## Requisitos de embalagem {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

A reprodução com o Flash Player requer os seguintes arquivos SWF:

* O arquivo SWF do aplicativo principal que manipula as APIs do Browser TVSDK.
* O arquivo SWF `playerProductInstall.swf` que lida com a instalação e atualizações do Flash Player.

Além disso, a reprodução de vídeo no Flash requer um arquivo de token de autorização que pode ser um arquivo SWF ou `.DAT`. O caminho para os arquivos SWF, o arquivo de token de autorização e o nome e tipo do arquivo de token podem ser especificados usando as APIs do AdobePSDK.

Por exemplo:

```js
// Set relative or http path to directory containing SWF.  
// Defaults to current directory for the html page. 
AdobePSDK.setSWFPath(<swfPath>); 
 
// Set the relative or http path to directory containing token file(s). 
// Defaults to SWFPath + "token/". 
AdobePSDK.setAuthorizationTokenPath(<authorizationTokenPath>); 
 
// Set the name of the token file, do not include any path in this string. 
AdobePSDK.setAuthorizationTokenFilename("hlsaf_localhost.swf"); 
 
//Set the token type, "DAT" or "SWF". Defaults to "DAT" 
AdobePSDK.setAuthorizationTokenType("SWF");
```

