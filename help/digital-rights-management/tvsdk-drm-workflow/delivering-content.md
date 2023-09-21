---
title: Entrega de conteúdo
description: Entrega de conteúdo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Entrega de conteúdo {#delivering-content}

O DRM do Primetime é agnóstico em relação ao mecanismo de entrega do conteúdo, pois o tempo de execução abstrai a camada de rede e simplesmente fornece o conteúdo protegido para o subsistema de DRM do Primetime. Assim, o conteúdo pode ser entregue por HTTP, HTTP Dynamic Streaming, RTMP ou RTMPE, HLS etc.

No entanto, dependendo do protocolo, pode haver complexidades envolvidas na recuperação dos metadados do conteúdo protegido ( `DRMContentData` - geralmente sob a forma de uma [!DNL .metadata] arquivo). Esses metadados DRM são necessários para chamar qualquer `DRMManager` API, como pré-busca de licença, autenticação DRM ou ingresso em um domínio de dispositivo. Por exemplo, com o protocolo RTMP/RTMPE, somente os dados FLV e F4V podem ser entregues ao cliente por meio do Flash Media Server (FMS). Por causa disso, o cliente deve recuperar o blob de metadados de outras maneiras. Uma opção para resolver esse problema é hospedar os metadados em um servidor Web HTTP e implementar o player de vídeo cliente para recuperar os metadados apropriados, dependendo do conteúdo que está sendo reproduzido.

```
private function getMetadata():void { 
    extrapolated-path-to-metadata = "https://metadatas.mywebserver.com/" + videoname; 
     var urlRequest : URLRequest =  
      new URLRequest(extrapolated-path-to-the-metadata + ".metadata");  
    var urlStream : URLStream = new URLStream();  
    urlStream.addEventListener(Event.COMPLETE, handleMetadata);  
    urlStream.addEventListener(IOErrorEvent.NETWORK_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.IO_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.VERIFY_ERROR, handleIOError);  
 
    try { 
        urlStream.load(urlRequest);  
    } catch(se:SecurityError) { 
        videoLog.text += se.toString() + "\n";  
    } catch(e:Error) { 
        videoLog.text += e.toString() + "\n";  
    } 
} 
```
