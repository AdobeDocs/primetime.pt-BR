---
description: O objeto DRMAuthenticateEvent é despachado quando um objeto Primetime tenta reproduzir conteúdo protegido que requer uma credencial de usuário para autenticação antes da reprodução (e a autenticação ainda não foi realizada). O manipulador DRMAuthenticateEvent é responsável por coletar as credenciais necessárias (nome de usuário, senha e tipo) e transmitir os valores para o método .setDRMAuthenticationCredentials() para validação.
title: Criar um manipulador DRMAuthenticateEvent
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Criar um manipulador DRMAuthenticateEvent{#create-a-drmauthenticateevent-handler}

O objeto DRMAuthenticateEvent é despachado quando um objeto Primetime tenta reproduzir conteúdo protegido que requer uma credencial de usuário para autenticação antes da reprodução (e a autenticação ainda não foi realizada). O manipulador DRMAuthenticateEvent é responsável por coletar as credenciais necessárias (nome de usuário, senha e tipo) e transmitir os valores para o método .setDRMAuthenticationCredentials() para validação.

O aplicativo deve fornecer algum mecanismo para obter credenciais do usuário. Por exemplo, o aplicativo pode fornecer a um usuário uma interface de usuário simples para inserir valores de nome de usuário e senha. Além disso, deve fornecer um mecanismo para lidar com e limitar tentativas repetidas de falha de autenticação.

Crie um manipulador de eventos que passe um conjunto de credenciais de autenticação embutidas para o objeto Primetime que originou o evento:

```
var connection:NetConnection = new NetConnection();  
connection.connect(null);  
var videoStream:Primetime = new Primetime(connection);  
 
videoStream.addEventListener( 
  DRMAuthenticateEvent.DRM_AUTHENTICATE,  
  drmAuthenticateEventHandler)  
  private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void {  
    videoStream.setDRMAuthenticationCredentials("administrator", "password", "drm");  
} 
```

(O código para reproduzir o vídeo e garantir que uma conexão bem-sucedida com o fluxo de vídeo não foi incluída aqui.)
