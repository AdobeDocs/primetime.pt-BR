---
description: Para usar o Flash Player, verifique se seu ambiente atende aos requisitos necessários.
title: Requisitos do Flash Player
exl-id: 26531d0d-d34c-4134-8a05-0604f00a3107
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Requisitos do Flash Player{#flash-player-requirements}

Para usar o Flash Player, verifique se seu ambiente atende aos requisitos necessários.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Estes são os requisitos para o Flash Player:

* Para reproduzir com `Primetime.js`, instale pelo menos a versão 23 do Flash Player.
* Para ser solicitado a fornecer atualizações para a versão 23 ou posterior do Flash Player, instale pelo menos a versão 11.0.0 do Flash Player.

## Requisitos de embalagem {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

A reprodução com o Flash Player requer os seguintes arquivos SWF:

* O principal arquivo de SWF do aplicativo que lida com APIs TVSDK do navegador.
* A variável `playerProductInstall.swf` Arquivo SWF que lida com a instalação e atualizações do Flash Player.

Além disso, a reprodução de vídeo no Flash requer um arquivo de token de autorização que pode ser um SWF ou um `.DAT` arquivo. O caminho para os arquivos SWF, o arquivo de token de autorização e o nome e tipo do arquivo de token podem ser especificados usando as APIs do Adobe PSDK.

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
