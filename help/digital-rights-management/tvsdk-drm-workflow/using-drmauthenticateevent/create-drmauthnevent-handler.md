---
description: O objeto DRMAuthenticateEvent é despachado quando um objeto do Primetime tenta reproduzir conteúdo protegido que requer uma credencial de usuário para autenticação antes da reprodução (e a autenticação ainda não foi executada). O manipulador DRMAuthenticateEvent é responsável por coletar as credenciais necessárias (nome de usuário, senha e tipo) e transmitir os valores para o método .setDRMAuthenticationCredentials() para validação.
title: Criar um manipulador DRMAuthenticateEvent
exl-id: fe01340b-8a76-4fd4-8c6c-85454d0e2218
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Criar um manipulador DRMAuthenticateEvent{#create-a-drmauthenticateevent-handler}

O objeto DRMAuthenticateEvent é despachado quando um objeto do Primetime tenta reproduzir conteúdo protegido que requer uma credencial de usuário para autenticação antes da reprodução (e a autenticação ainda não foi executada). O manipulador DRMAuthenticateEvent é responsável por coletar as credenciais necessárias (nome de usuário, senha e tipo) e transmitir os valores para o método .setDRMAuthenticationCredentials() para validação.

O aplicativo deve fornecer algum mecanismo para a obtenção de credenciais de usuário. Por exemplo, o aplicativo pode fornecer ao usuário uma interface simples para inserir valores de nome de usuário e senha. Além disso, ele deve fornecer um mecanismo para lidar com tentativas repetidas de falha de autenticação e limitá-las.

Crie um manipulador de eventos que passe um conjunto de credenciais de autenticação embutidas em código para o objeto do Primetime que originou o evento:

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

(O código para reproduzir o vídeo e garantir que uma conexão bem-sucedida com o fluxo de vídeo tenha sido feita não está incluído aqui.)
