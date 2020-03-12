---
description: O objeto DRMAuthenticateEvent é despachado quando um objeto Primetime tenta reproduzir conteúdo protegido que requer uma credencial de usuário para autenticação antes da reprodução (e a autenticação ainda não foi executada). O manipulador DRMAuthenticateEvent é responsável por coletar as credenciais necessárias (nome de usuário, senha e tipo) e transmitir os valores para o método .setDRMAuthenticationCredentials() para validação.
seo-description: O objeto DRMAuthenticateEvent é despachado quando um objeto Primetime tenta reproduzir conteúdo protegido que requer uma credencial de usuário para autenticação antes da reprodução (e a autenticação ainda não foi executada). O manipulador DRMAuthenticateEvent é responsável por coletar as credenciais necessárias (nome de usuário, senha e tipo) e transmitir os valores para o método .setDRMAuthenticationCredentials() para validação.
seo-title: Criar um manipulador DRMAuthenticateEvent
title: Criar um manipulador DRMAuthenticateEvent
uuid: 58330691-d0b5-46bd-9b1d-8dc597580d31
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# Criar um manipulador DRMAuthenticateEvent{#create-a-drmauthenticateevent-handler}

O objeto DRMAuthenticateEvent é despachado quando um objeto Primetime tenta reproduzir conteúdo protegido que requer uma credencial de usuário para autenticação antes da reprodução (e a autenticação ainda não foi executada). O manipulador DRMAuthenticateEvent é responsável por coletar as credenciais necessárias (nome de usuário, senha e tipo) e transmitir os valores para o método .setDRMAuthenticationCredentials() para validação.

O aplicativo deve fornecer algum mecanismo para obter as credenciais do usuário. Por exemplo, o aplicativo pode fornecer a um usuário uma interface de usuário simples para inserir valores de nome de usuário e senha. Além disso, deve fornecer um mecanismo para lidar com e limitar tentativas repetidas de falha de autenticação.

Crie um manipulador de eventos que passe um conjunto de credenciais de autenticação codificadas permanentemente para o objeto Primetime que originou o evento:

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

(O código para reproduzir o vídeo e verificar se uma conexão bem-sucedida com o fluxo de vídeo foi feita não está incluído aqui.)
