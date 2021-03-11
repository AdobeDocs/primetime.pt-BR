---
description: Definir políticas é o processo de especificar condições para quando e como um usuário tem permissão para reproduzir conteúdo de vídeo protegido.
title: Configuração de políticas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Definindo políticas{#setting-policies}

Definir políticas é o processo de especificar condições para quando e como um usuário tem permissão para reproduzir conteúdo de vídeo protegido.

A criação de política ocorre como parte da solicitação de token de licença. (Consulte [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) para obter um exemplo usando Widevine).

Depois que o código do lado do servidor de um cliente determinar que ele emitirá uma licença (com base em verificações de direitos, geolocalização ou qualquer outra informação necessária), ele solicitará um token e *no token* especificará os `securityLevel`, `hdcpOutputControl` e `licenseDuration` necessários. Essas são as opções do lado do cliente para uma política de Widevine. Outras soluções de DRM oferecem abordagens semelhantes, mas os detalhes são diferentes em cada caso e são desenvolvidos nos fluxos de trabalho individuais.

>[!NOTE]
>
>O Adobe fornece um exemplo de servidor de referência que mostra como implementar seu próprio servidor de direito/vitrine: [Servidor de referência: Exemplo de SEES (ExpressPlay Entitlement Server)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

