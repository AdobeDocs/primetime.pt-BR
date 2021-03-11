---
description: Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.
title: Métricas de faturamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Visão geral {#billing-metrics-overview}

Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.

Toda vez que o reprodutor gera um evento de início de fluxo, o TVSDK do Navegador é iniciado para enviar mensagens HTTP periodicamente para o sistema de faturamento do Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, VOD pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com o Adobe determina os valores reais.

As mensagens contêm as seguintes informações:

* Tipo de conteúdo (ao vivo, linear ou VOD)
* URL do conteúdo
* Se os anúncios estão ativados
* Se os anúncios intermediários estão ativados (somente VOD)
* Se o fluxo está protegido pelo DRM
* A versão e a plataforma do TVSDK do navegador

O Adobe pré-configura esse acordo, mas se você quiser alterar o acordo, trabalhe com seu representante de Ativação do Adobe.

Para monitorar as estatísticas que o TVSDK do navegador envia para o Adobe, obtenha o URL do seu representante de Ativação do Adobe e use uma ferramenta de captura de rede, por exemplo, Charles, para ver os dados.
