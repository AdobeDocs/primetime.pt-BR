---
description: Com o TVSDK, você pode controlar a experiência básica de reprodução para vídeo ao vivo e sob demanda (VOD). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.
seo-description: Com o TVSDK, você pode controlar a experiência básica de reprodução para vídeo ao vivo e sob demanda (VOD). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.
seo-title: Aguardar um estado válido
title: Aguardar um estado válido
uuid: 22b68162-1625-4e8a-8566-b0c198155622
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Aguarde um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução para vídeo ao vivo e sob demanda (VOD). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.

Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um estado válido.
O jogador passa por vários estados. Aguardar o player no estado correto garante que o recurso de mídia tenha sido carregado com êxito. Se o player não estiver no estado necessário, muitos métodos do player lançam `IllegalStateException`.

O estado necessário geralmente é PREPARADO.
