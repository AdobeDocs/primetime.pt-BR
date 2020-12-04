---
seo-title: Opções de implantação do License Server
title: Opções de implantação do License Server
uuid: 297c587f-23e2-4bb5-911b-72d7b82370f4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Opções de implantação do License Server{#license-server-deployment-options}

O License Server pode ser implantado usando uma das seguintes opções:

* **Adobe Access Server for Protected Streaming** — Este License Server é otimizado para streaming. Por exemplo, você pode configurar o servidor para Adobe com Adobe Access. Esse servidor pode ser implantado facilmente com uma configuração muito pequena, além de suportar vários locatários, e pode alcançar um alto nível de escalabilidade. No entanto, como essa implementação é otimizada para streaming, ela não oferece suporte aos recursos completos de acesso ao Adobe. Por exemplo, autenticação de nome de usuário/senha, domínios e encadeamento de licença não são suportados. As regras de uso nas licenças emitidas por esse servidor são controladas por meio de um arquivo de configuração do servidor, que substitui a política usada no momento do empacotamento. Consulte o *Adobe Access Server for Protected Streaming Guide* para obter mais detalhes sobre as regras de uso suportadas por este servidor.
* **Servidor**  de Licenças de Implementação de Referência— Utilize esta configuração como ponto de partida para uma implementação de servidor personalizado. Este é um exemplo de implementação do servidor de licenças, incluindo o código fonte, que demonstra como usar as APIs no SDK de acesso ao Adobe para lidar com todos os tipos de solicitações e como implementar uma lógica comercial personalizada suportada por um banco de dados. As regras de uso nas licenças emitidas por esse servidor são controladas pela política associada ao conteúdo no momento do empacotamento.
* **Implementação**  personalizada do servidor— Você também pode implementar seu próprio servidor de licenciamento usando o SDK. As informações neste capítulo descrevem as APIs usadas para implementar um servidor de licenças.

