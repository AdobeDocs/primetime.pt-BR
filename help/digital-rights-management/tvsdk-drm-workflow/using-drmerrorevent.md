---
seo-title: Uso da visão geral da classe DRMErrorEvent
title: Uso da visão geral da classe DRMErrorEvent
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Uso da classe DRMErrorEvent {#using-the-drmerrorevent-class}

O Primetime despacha um `DRMErrorEvent` objeto quando um objeto Primetime, tentando reproduzir conteúdo protegido, encontra um erro [relacionado ao](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM. Se as credenciais do usuário forem inválidas, o `DRMAuthenticateEvent` objeto será despachado repetidamente até que o usuário insira credenciais válidas ou o aplicativo negue mais tentativas. O aplicativo é responsável por ouvir outros eventos de erro de DRM para detectar, identificar e manipular os erros [relacionados ao](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM.

Mesmo com credenciais de usuário válidas, os termos da licença do conteúdo ainda podem impedir que um usuário visualize o conteúdo criptografado. Por exemplo, o acesso de um usuário pode ser negado por tentar visualização de conteúdo em um aplicativo não autorizado (por exemplo, listagem de Permissão de aplicativo). Um aplicativo não autorizado é aquele que não foi assinado com um Certificado de assinatura de aplicativo listado como permitido. Nesse caso, um `DRMErrorEvent` objeto é despachado.

eventos de erro também podem ser disparados se o conteúdo estiver corrompido ou se a versão do aplicativo não corresponder ao que a licença especifica. O aplicativo deve fornecer um mecanismo adequado para lidar com erros.

## Criar um manipulador DRMErrorEvent {#create-a-drmerrorevent-handler}

Crie um manipulador de eventos para processar eventos de erro despachados do Primetime quando ele encontrar um erro ao tentar reproduzir conteúdo protegido.

Normalmente, quando um aplicativo encontra um erro, ele executa qualquer número de tarefas de limpeza. Em seguida, informa o usuário do erro e fornece opções para resolver o problema.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
