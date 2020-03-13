---
seo-title: Fornecer conteúdo
title: Fornecer conteúdo
uuid: b277d369-fee3-4a20-9dd8-27b3a8a82a9e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Fornecer conteúdo {#delivering-content}

O Primetime DRM é agnóstico ao mecanismo de entrega do conteúdo, já que o tempo de execução abstrai a camada de rede e simplesmente fornece o conteúdo protegido ao subsistema Primetime DRM. Portanto, o conteúdo pode ser entregue por HTTP, HTTP Dynamic Streaming, RTMP ou RTMPE, HLS etc.

No entanto, dependendo do protocolo, pode haver complicações na recuperação dos metadados do conteúdo protegido ( `DRMContentData` - normalmente na forma de um [!DNL .metadata] arquivo carregado no lado). Esses metadados DRM são necessários para chamar qualquer `DRMManager` API, como pré-buscar a licença, autenticação DRM ou ingressar em um domínio de dispositivo. Por exemplo, com o protocolo RTMP/RTMPE, somente os dados FLV e F4V podem ser entregues ao cliente por meio do Flash Media Server (FMS). Por isso, o cliente deve recuperar o blob de metadados de outras maneiras. Uma opção para resolver esse problema é hospedar os metadados em um servidor da Web HTTP e implementar o player de vídeo cliente para recuperar os metadados apropriados, dependendo do conteúdo que está sendo reproduzido.

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

