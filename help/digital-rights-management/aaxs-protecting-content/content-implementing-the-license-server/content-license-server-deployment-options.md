---
title: Opções de implantação do License Server
description: Opções de implantação do License Server
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Opções de implantação do License Server{#license-server-deployment-options}

O License Server pode ser implantado usando uma das seguintes opções:

* **Adobe Access Server for Protected Streaming**  — Este License Server é otimizado para streaming. Por exemplo, você pode configurar o servidor para Adobe HTTP Dynamic Streaming com Adobe Access. Esse servidor pode ser implantado facilmente, com pouca configuração necessária e terá suporte para vários locatários, além de alcançar um alto nível de escalabilidade. No entanto, como essa implementação é otimizada para streaming, ela não suporta todos os recursos de Acesso ao Adobe. Por exemplo, autenticação de nome de usuário/senha, domínios e cadeia de licença não são compatíveis. As regras de uso nas licenças emitidas por este servidor são controladas por meio de um arquivo de configuração do servidor, que substitui a política usada no momento do empacotamento. Consulte o *Adobe Access Server for Protected Streaming Guide* para obter mais detalhes sobre as regras de uso suportadas por este servidor.
* **Servidor de Licenças de Implementação de Referência**  — Utilize esta configuração como ponto de partida para uma implementação de servidor personalizado. Este é um exemplo de implementação do servidor de licenças, incluindo o código-fonte, que demonstra como usar as APIs no SDK de acesso do Adobe para lidar com todos os tipos de solicitações e como implementar a lógica comercial personalizada apoiada por um banco de dados. As regras de uso nas licenças emitidas por este servidor são controladas por meio da política associada ao conteúdo no momento do empacotamento.
* **Implementação**  do servidor personalizado — você também pode implementar seu próprio servidor de licenciamento usando o SDK. As informações neste capítulo descrevem as APIs usadas para implementar um servidor de licenças.

