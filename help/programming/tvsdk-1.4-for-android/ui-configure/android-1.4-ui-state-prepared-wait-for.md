---
description: Com o TVSDK, você pode controlar a experiência básica de reprodução de vídeo sob demanda (VOD). O TVSDK fornece métodos e propriedades na instância do reprodutor que você pode usar para configurar a interface do usuário do reprodutor.
title: Aguardar um estado válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Aguarde um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução de vídeo sob demanda (VOD). O TVSDK fornece métodos e propriedades na instância do reprodutor que você pode usar para configurar a interface do usuário do reprodutor.

Antes de usar a maioria dos métodos do reprodutor TVSDK, o reprodutor deve estar em um estado válido.
O reprodutor passa por vários estados. Aguardar o estado correto do reprodutor garante que este tenha sido carregado com êxito. Se o reprodutor não estiver no estado exigido, muitos métodos do reprodutor exibirão `IllegalStateException`.

O estado necessário geralmente é PREPARADO.
