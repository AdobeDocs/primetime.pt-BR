---
title: Opções de implantação do License Server
description: Opções de implantação do License Server
copied-description: true
exl-id: c7422a8f-2cd1-4ace-8706-eb3e5a55eac6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Opções de implantação do License Server{#license-server-deployment-options}

O License Server pode ser implantado usando uma das seguintes opções:

* **Adobe Access Server para transmissão protegida** — Este License Server foi otimizado para streaming. Por exemplo, você pode configurar o servidor para o HTTP Dynamic Streaming do Adobe com Acesso ao Adobe. Esse servidor pode ser implantado facilmente com pouca configuração necessária, oferecerá suporte a vários locatários e poderá alcançar um alto nível de escalabilidade. No entanto, como essa implementação é otimizada para transmissão, ela não oferece suporte aos recursos completos de Acesso ao Adobe. Por exemplo, autenticação de nome de usuário/senha, domínios e encadeamento de licenças não são compatíveis. As regras de uso nas licenças emitidas por este servidor são controladas por meio de um arquivo de configuração do servidor, que substitui a política usada no momento do empacotamento. Consulte a *Guia do Adobe Access Server para transmissão protegida* para obter mais detalhes sobre as regras de uso aceitas por este servidor.
* **Referência do servidor de licenças de implementação** — Use esta configuração como ponto de partida para uma implementação de servidor personalizado. Este é um exemplo de implementação de servidor de licença, incluindo código-fonte, que demonstra como usar as APIs no SDK do Adobe Access para lidar com todos os tipos de solicitações e como implementar uma lógica de negócios personalizada apoiada por um banco de dados. As regras de uso nas licenças emitidas por este servidor são controladas por meio da política associada ao conteúdo no momento do empacotamento.
* **Implementação de servidor personalizado** — Você também pode implementar seu próprio servidor de licenciamento usando o SDK. As informações neste capítulo descrevem as APIs usadas para implementar um servidor de licenças.
