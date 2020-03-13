---
seo-title: Uso da visão geral da classe DRMErrorEvent
title: Uso da visão geral da classe DRMErrorEvent
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Uso da visão geral da classe DRMErrorEvent {#using-the-drmerrorevent-class-overview}

O Primetime despacha um `DRMErrorEvent` objeto quando um objeto Primetime, tentando reproduzir conteúdo protegido, encontra um erro [relacionado ao](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM. Se as credenciais do usuário forem inválidas, o `DRMAuthenticateEvent` objeto será despachado repetidamente até que o usuário insira credenciais válidas ou o aplicativo negue mais tentativas. O aplicativo é responsável por ouvir outros eventos de erro de DRM para detectar, identificar e manipular os erros [relacionados ao](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM.

Mesmo com credenciais de usuário válidas, os termos da licença do conteúdo ainda podem impedir que um usuário visualize o conteúdo criptografado. Por exemplo, é possível negar o acesso de um usuário para tentar exibir o conteúdo em um aplicativo não autorizado (por exemplo, Lista de permissões do aplicativo). Um aplicativo não autorizado é aquele que não foi assinado com um Certificado de assinatura de aplicativo na lista de permissões. Nesse caso, um `DRMErrorEvent` objeto é despachado.

Os eventos de erro também podem ser disparados se o conteúdo estiver corrompido ou se a versão do aplicativo não corresponder ao que a licença especifica. O aplicativo deve fornecer um mecanismo adequado para lidar com erros.
