---
title: Uso da visão geral da classe DRMErrorEvent
description: Uso da visão geral da classe DRMErrorEvent
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Uso da visão geral da classe DRMErrorEvent {#using-the-drmerrorevent-class-overview}

O Primetime despacha um objeto `DRMErrorEvent` quando um objeto Primetime, tentando reproduzir conteúdo protegido, encontra um [erro relacionado ao DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Se as credenciais do usuário forem inválidas, o objeto `DRMAuthenticateEvent` será despachado repetidamente até que o usuário insira credenciais válidas ou o aplicativo negue mais tentativas. O aplicativo é responsável por ouvir qualquer outro evento de erro de DRM para detectar, identificar e manipular os [erros relacionados ao DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Mesmo com credenciais de usuário válidas, os termos da licença do conteúdo ainda podem impedir que um usuário visualize o conteúdo criptografado. Por exemplo, um usuário pode ter acesso negado por tentar visualizar o conteúdo em um aplicativo não autorizado (por exemplo, lista de Permissões de aplicativo). Um aplicativo não autorizado é aquele que não foi assinado com um Certificado de assinatura de aplicativo listado como permitido. Nesse caso, um objeto `DRMErrorEvent` é despachado.

Eventos de erro também podem ser disparados se o conteúdo estiver corrompido ou se a versão do aplicativo não corresponder ao que a licença especifica. O pedido deve prever um mecanismo adequado para o tratamento de erros.
