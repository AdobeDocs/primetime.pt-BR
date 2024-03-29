---
description: A definição de políticas é o processo de especificar condições para quando e como um usuário tem permissão para reproduzir conteúdo de vídeo protegido.
title: Definição de políticas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Definição de políticas{#setting-policies}

A definição de políticas é o processo de especificar condições para quando e como um usuário tem permissão para reproduzir conteúdo de vídeo protegido.

A criação da política ocorre como parte da solicitação de token de licença. (Consulte [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) por exemplo, usando Widevine).

Depois que o código do lado do servidor do cliente determinar que emitirá uma licença (com base em verificações de direitos, geolocalização ou qualquer outra informação necessária), ele solicitará um token e *no token* especifica os parâmetros `securityLevel`, `hdcpOutputControl`, e `licenseDuration`. Essas são as opções do lado do cliente para uma política Widevine. Outras soluções de DRM oferecem abordagens semelhantes, mas os detalhes são diferentes em cada caso e são elaborados nos workflows individuais.

>[!NOTE]
>
>O Adobe fornece um exemplo de servidor de referência que mostra como implementar seu próprio servidor de direitos/vitrine: [Servidor de Referência: Exemplo de Servidor de Direitos ExpressPlay (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)
