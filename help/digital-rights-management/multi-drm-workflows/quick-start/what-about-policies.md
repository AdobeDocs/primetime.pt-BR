---
description: Definir políticas é o processo de especificar condições para quando e como um usuário pode reproduzir conteúdo de vídeo protegido.
seo-description: Definir políticas é o processo de especificar condições para quando e como um usuário pode reproduzir conteúdo de vídeo protegido.
seo-title: Definindo políticas
title: Definindo políticas
uuid: 2d2672ce-5ed4-4868-aa5e-0a9e21a809b3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Definindo políticas{#setting-policies}

Definir políticas é o processo de especificar condições para quando e como um usuário pode reproduzir conteúdo de vídeo protegido.

A criação de política ocorre como parte da solicitação de token de licença. (Consulte [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) para obter um exemplo usando o Widevine).

Depois que o código do lado do servidor do cliente determinar que ele emitirá uma licença (com base em verificações de direitos, localização geográfica ou quaisquer outras informações necessárias), ele solicitará um token e, *no token* , especificará o necessário `securityLevel`, `hdcpOutputControl`e `licenseDuration`. Essas são as opções do lado do cliente para uma política de Widevine. Outras soluções de DRM oferecem abordagens semelhantes, mas os detalhes são diferentes em cada caso e são desenvolvidos nos fluxos de trabalho individuais.

>[!NOTE]
>
>A Adobe fornece um exemplo de servidor de referência que mostra como implementar seu próprio servidor de direito / vitrine: Servidor [de referência: Servidor de direito ExpressPlay de amostra (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

