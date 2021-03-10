---
description: Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.
title: Métricas de faturamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Visão geral {#billing-metrics-overview}

Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.

Toda vez que gera um evento de início de fluxo, o TVSDK inicia periodicamente mensagens HTTP para enviar mensagens HTTP ao sistema de faturamento do Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, VOD pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com o Adobe determina os valores reais.

As mensagens contêm as seguintes informações:

* Tipo de conteúdo (ao vivo, linear ou VOD)
* URL do conteúdo
* Se os anúncios estão ativados
* Se os anúncios intermediários estão ativados (somente VOD)
* Se o fluxo está protegido pelo DRM
* A versão e a plataforma do TVSDK

O Adobe predefine esse acordo, mas você pode trabalhar com seu representante de Ativação do Adobe para alterar o acordo, trabalhar com seu representante de Ativação do Adobe.

Para monitorar as estatísticas que o TVSDK envia para o Adobe, obtenha o URL do representante de Ativação do Adobe e use uma ferramenta de captura de rede, como o Charles, para ver os dados.
