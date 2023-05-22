---
title: Uso da visão geral da classe DRMErrorEvent
description: Uso da visão geral da classe DRMErrorEvent
copied-description: true
exl-id: c651cdcf-f8f8-4085-a88e-d82030f90f11
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Uso da classe DRMErrorEvent {#using-the-drmerrorevent-class}

O Primetime despacha um `DRMErrorEvent` objeto quando um objeto do Primetime, tentando reproduzir conteúdo protegido, encontra um [Erro relacionado ao DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Se as credenciais do usuário forem inválidas, a variável `DRMAuthenticateEvent` O objeto envia repetidamente até que o usuário insira credenciais válidas ou o aplicativo negue outras tentativas. O aplicativo é responsável por ouvir qualquer outro evento de erro DRM para detectar, identificar e manipular a [Erros relacionados ao DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Mesmo com credenciais de usuário válidas, os termos da licença do conteúdo ainda podem impedir que um usuário visualize o conteúdo criptografado. Por exemplo, o acesso de um usuário pode ser negado para tentar visualizar o conteúdo em um aplicativo não autorizado (por exemplo, a Lista de permissões de aplicativos). Um aplicativo não autorizado é aquele que não foi assinado com um Certificado de Autenticação de Aplicativo incluído na lista de permissões. Neste caso, uma `DRMErrorEvent` objeto é despachado.

Eventos de erro também podem ser acionados se o conteúdo estiver corrompido ou se a versão do aplicativo não corresponder ao que a licença especifica. O aplicativo deve fornecer um mecanismo apropriado para tratar erros.

## Criar um manipulador DRMErrorEvent {#create-a-drmerrorevent-handler}

Crie um manipulador de eventos para processar eventos de erro despachados do Primetime quando ele encontrar um erro ao tentar reproduzir conteúdo protegido.

Normalmente, quando um aplicativo encontra um erro, ele executa qualquer número de tarefas de limpeza. Em seguida, ele informa o usuário sobre o erro e fornece opções para resolver o problema.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
