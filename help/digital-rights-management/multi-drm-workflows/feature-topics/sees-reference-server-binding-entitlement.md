---
description: O servidor de referência SEES mostra como ativar o serviço de direito de vinculação de dispositivo usando o ExpressPlay.
seo-description: O servidor de referência SEES mostra como ativar o serviço de direito de vinculação de dispositivo usando o ExpressPlay.
seo-title: Direito de Vínculo de Dispositivo do Serviço de Referência
title: Direito de Vínculo de Dispositivo do Serviço de Referência
uuid: 22ce2f8e-1758-4528-8caf-60d209839afe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Serviço de referência: Direito de vinculação de dispositivo {#reference-service-device-binding-entitlement}

O servidor de referência SEES mostra como ativar o serviço de direito de vinculação de dispositivo usando o ExpressPlay.

>[!NOTE]
>
>O serviço de direito vinculado ao dispositivo também pode ser vinculado ao tempo ou fornecer duração de aluguel.

Para inicializar as informações `device_id`, reproduza um conteúdo simulado M3U8. Em seguida, você pode incorporar um cookie no token ExpressPlay, gerar um SPC (que contém `device_id`) e enviar um `getToken` para o ExpressPlay Server.

![](assets/fees-device-binding.png)

A sequência start tocando um manequim M3U8. Um cookie é enviado para o servidor SEES para obter o URL do token ExpressPlay. Depois de receber o URL do token ExpressPlay vinculado ao cookie, a próxima etapa é gerar o SPC e enviá-lo para o ExpressPlay Server. O servidor ExpressPlay extrai o `device_id` do SPC, o cookie do URL do token ExpressPlay e coloca o cookie e `device_id` no log de transações.

O cliente faz uma solicitação de licença real para SEES enviar o mesmo cookie. O SEES emprega o cookie para recuperar o `device_id` do servidor ExpressPlay.

O SEES solicita um token ExpressPlay vinculado ao dispositivo, bem como um limite de tempo, e retorna esse token ao cliente.

O cliente faz a solicitação de licença com o token ExpressPlay.

O servidor ExpressPlay compara o `device_id` no SPC com o `device_id` no token ExpressPlay. O servidor ExpressPlay só emite uma licença se os dois valores `device_id` corresponderem.
