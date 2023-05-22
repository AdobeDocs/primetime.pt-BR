---
description: O servidor de referência do SEES mostra como ativar o serviço de direito de ligação de dispositivos usando o ExpressPlay.
title: Direito de vinculação de dispositivo do serviço de referência
exl-id: 91f9d406-f3f9-47d3-aa50-f47c4e81b9fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Serviço de Referência: Direito de Vinculação de Dispositivo {#reference-service-device-binding-entitlement}

O servidor de referência do SEES mostra como ativar o serviço de direito de ligação de dispositivos usando o ExpressPlay.

>[!NOTE]
>
>O serviço de direito vinculado ao dispositivo também pode ser vinculado ao tempo ou fornecer duração do aluguel.

Para inicializar o `device_id` informações, reproduzir um conteúdo M3U8 fictício. Você pode então incorporar um cookie no token ExpressPlay, gerar um SPC (que contém o cookie `device_id`) e enviar um `getToken` para o servidor ExpressPlay.

![](assets/fees-device-binding.png)

A sequência começa reproduzindo um M3U8 fictício. Um cookie é enviado ao servidor SEES para obter o URL do token ExpressPlay. Depois de receber o URL do token ExpressPlay vinculado a cookies, o próximo passo é gerar o SPC e enviá-lo para o ExpressPlay Server. O servidor ExpressPlay extrai o `device_id` do SPC, o cookie do URL do token ExpressPlay, e coloca o cookie e `device_id` no log de transações.

O cliente faz uma solicitação de licença real para o SEES enviar o mesmo cookie. O SEES emprega o cookie para recuperar o `device_id` do servidor ExpressPlay.

O SEES solicita um token ExpressPlay vinculado a dispositivos, bem como a tempo, e retorna esse token ao cliente.

O cliente faz a solicitação de licença com o token ExpressPlay.

O servidor ExpressPlay compara o `device_id` no RCM com a `device_id` no token ExpressPlay. O servidor ExpressPlay só emitirá uma licença se os dois `device_id` os valores de correspondem.
