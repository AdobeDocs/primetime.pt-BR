---
description: Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.
seo-description: Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.
seo-title: Métricas de faturamento
title: Métricas de faturamento
uuid: e09b77b3-89d3-44d6-be4e-e1612fbf89fc
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Visão geral {#billing-metrics-overview}

Para acomodar clientes que desejam pagar apenas pelo que usam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta métricas de uso e usa essas métricas para determinar quanto faturar os clientes.

Toda vez que o player gera um evento de start de fluxo, start TVSDK do navegador enviam mensagens HTTP periodicamente para o sistema de cobrança do Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, VOD pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com a Adobe determina os valores reais.

As mensagens contêm as seguintes informações:

* Tipo de conteúdo (ao vivo, linear ou VOD)
* URL do conteúdo
* Se os anúncios estão ativados
* Se os anúncios intermediários estão ativados (apenas VOD)
* Se o fluxo é protegido pelo DRM
* A versão e a plataforma do TVSDK do navegador

O Adobe pré-configura essa organização, mas se você quiser alterar a organização, trabalhe com seu representante de Ativação do Adobe.

Para monitorar as estatísticas que o TVSDK do navegador envia para o Adobe, obtenha o URL do seu representante de Ativação do Adobe e use uma ferramenta de captura de rede, por exemplo, Charles, para ver os dados.
