---
description: Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, a Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.
seo-description: Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, a Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.
seo-title: Métricas de faturamento
title: Métricas de faturamento
uuid: 4a03995a-60f6-440e-9cdf-9c0b9c5f1d90
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Visão geral {#billing-metrics-overview}

Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, a Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.

Toda vez que o player gera um evento de início de fluxo, o TVSDK começa a enviar mensagens HTTP periodicamente para o sistema de cobrança da Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, VOD pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com a Adobe determina os valores reais.

As mensagens contêm as seguintes informações:

* Tipo de conteúdo (ao vivo, linear ou VOD)
* URL do conteúdo
* Se os anúncios estão ativados
* Se os anúncios intermediários estão ativados (apenas VOD)
* Se o fluxo é protegido pelo DRM
* A versão e a plataforma do TVSDK

A Adobe pré-configura essa organização, mas você pode trabalhar com seu representante do Adobe Enablement para alterar a organização e trabalhar com seu representante do Adobe Enablement.

Para monitorar as estatísticas que o TVSDK envia para a Adobe, obtenha o URL do seu representante do Adobe Enablement e use uma ferramenta de captura de rede, como Charles, para ver os dados.
