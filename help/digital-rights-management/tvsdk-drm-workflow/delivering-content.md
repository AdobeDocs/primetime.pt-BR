---
title: Entrega de conteúdo
description: Entrega de conteúdo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Fornecer conteúdo {#delivering-content}

O DRM do Primetime é independente do mecanismo de entrega do conteúdo, pois o tempo de execução abstrai a camada de rede e simplesmente fornece o conteúdo protegido para o subsistema DRM do Primetime. Portanto, o conteúdo pode ser entregue por HTTP, HTTP Dynamic Streaming, RTMP ou RTMPE, HLS etc.

No entanto, dependendo do protocolo, pode haver complexidades envolvidas na recuperação dos metadados do conteúdo protegido ( `DRMContentData` - normalmente no formato de um arquivo [!DNL .metadata] carregado lado). Esses metadados de DRM são necessários para chamar qualquer API `DRMManager`, como pré-buscar a licença, autenticação de DRM ou ingressar em um domínio de dispositivo. Por exemplo, com o protocolo RTMP/RTMPE, somente os dados FLV e F4V podem ser entregues ao cliente por meio do Flash Media Server (FMS). Por causa disso, o cliente deve recuperar o blob de metadados de outras maneiras. Uma opção para resolver esse problema é hospedar os metadados em um servidor da Web HTTP e implementar o reprodutor de vídeo do cliente para recuperar os metadados apropriados, dependendo do conteúdo que está sendo reproduzido.

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

