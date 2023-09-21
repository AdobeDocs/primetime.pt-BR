---
description: Com o TVSDK, você pode controlar a experiência básica de reprodução para VOD (live and video on demand). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.
title: Aguardar um estado válido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Aguardar um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução para VOD (live and video on demand). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.

Antes de usar a maioria dos métodos do reprodutor TVSDK, o reprodutor deve estar em um estado válido.
O reprodutor passa por vários estados. Aguardar o reprodutor para estar no estado correto garante que o recurso de mídia foi carregado com êxito. Se o reprodutor não estiver pelo menos no estado obrigatório, muitos métodos de reprodutor acionarão `IllegalStateException`.

O estado obrigatório é geralmente PREPARADO.
