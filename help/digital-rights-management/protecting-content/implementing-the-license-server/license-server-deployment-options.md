---
seo-title: Opções de implantação do License Server
title: Opções de implantação do License Server
uuid: 732b948f-8037-423e-9f85-770d6316cbae
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Opções de implantação do License Server{#license-server-deployment-options}

Você pode implantar o License Server usando uma das seguintes opções:

* Adobe Primetime DRM Server for Protected Streaming — Este License Server é otimizado para streaming. Por exemplo, você pode configurar o servidor para o Adobe com o Primetime DRM. Esse servidor pode ser implantado facilmente com uma configuração muito pequena, necessária, e oferece suporte para vários locatários. Ele pode alcançar um alto nível de escalabilidade. Como essa implementação é otimizada para streaming, ela não suporta todos os recursos do Primetime DRM. Por exemplo, autenticação de nome de usuário/senha, domínios e encadeamento de licença não são suportados. As regras de uso nas licenças emitidas por esse servidor são controladas por meio de um arquivo de configuração do servidor, que substitui a política usada no momento do empacotamento.

   Consulte o *Adobe Primetime DRM Server for Protected Streaming Guide* para obter mais detalhes sobre as regras de uso suportadas pelo servidor de licenças.
* Servidor de Licenças de Implementação de Referência — Você pode usar esta configuração para personalizar a implementação do servidor. Este é um exemplo de implementação do servidor de licenças, incluindo o código fonte, que demonstra como usar as APIs no SDK do DRM Primetime para gerenciar todos os tipos de solicitações e como implementar uma lógica comercial personalizada suportada por um banco de dados. As regras de uso nas licenças emitidas por esse servidor são controladas pela política associada ao conteúdo no momento do empacotamento.
* Implementação personalizada do servidor — Você também pode implementar seu próprio servidor de licenciamento com o SDK. As informações descrevem como as APIs são usadas para implementar um servidor de licenças.

