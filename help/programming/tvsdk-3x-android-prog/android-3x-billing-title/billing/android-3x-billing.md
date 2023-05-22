---
description: Para acomodar os clientes que desejam pagar apenas pelo que utilizam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta as métricas de uso e as utiliza para determinar quanto faturar aos clientes.
title: Métricas de cobrança
exl-id: 6e839f59-dd1e-4037-96a9-8b35b361988f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Métricas de cobrança {#billing-metrics}

Para acomodar os clientes que desejam pagar apenas pelo que utilizam, em vez de uma taxa fixa independentemente do uso real, o Adobe coleta as métricas de uso e as utiliza para determinar quanto faturar aos clientes.

Toda vez que o reprodutor gera um evento de início de fluxo, o TVSDK começa a enviar mensagens HTTP periodicamente para o sistema de cobrança do Adobe. O período, conhecido como duração faturável, pode ser diferente para VOD padrão, pro VOD (anúncios intermediários ativados) e conteúdo ao vivo. A duração padrão para cada tipo de conteúdo é de 30 minutos, mas seu contrato com a Adobe determina os valores reais.

As mensagens contêm as seguintes informações:

* Tipo de conteúdo (ao vivo, linear ou VOD)
* URL de conteúdo
* Se os anúncios estão habilitados
* Se os anúncios intermediários estão ativados (somente VOD)
* Se o fluxo está protegido por DRM
* A versão e a plataforma do TVSDK

O Adobe pré-configura essa organização, mas você pode trabalhar com o representante de Ativação de Adobe para alterar a organização e trabalhar com o representante de Ativação de Adobe.

Para monitorar as estatísticas que o TVSDK envia para o Adobe, obtenha o URL do seu representante de Ativação de Adobe e use uma ferramenta de captura de rede, como o Charles, para ver os dados.
