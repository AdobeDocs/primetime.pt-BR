---
title: Opções de implantação do License Server
description: Opções de implantação do License Server
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Opções de implantação do License Server{#license-server-deployment-options}

Você pode implantar o License Server usando uma das seguintes opções:

* Adobe Primetime DRM Server for Protected Streaming — Este License Server é otimizado para streaming. Por exemplo, você pode configurar o servidor para o Adobe com o Primetime DRM. Esse servidor pode ser implantado facilmente com pouca configuração necessária e oferece suporte a vários locatários. Ele pode alcançar um alto nível de escalabilidade. Como essa implementação é otimizada para streaming, ela não suporta todos os recursos de DRM do Primetime. Por exemplo, autenticação de nome de usuário/senha, domínios e cadeia de licença não são compatíveis. As regras de uso nas licenças emitidas por este servidor são controladas por meio de um arquivo de configuração do servidor, que substitui a política usada no momento do empacotamento.

   Consulte o *Adobe Primetime DRM Server for Protected Streaming Guide* para obter mais detalhes sobre as regras de uso compatíveis com o servidor de licenças.
* Servidor de Licenças de Implementação de Referência — Você pode usar esta configuração para personalizar sua implementação do servidor. Este é um exemplo de implementação do servidor de licenças, incluindo o código-fonte, que demonstra como usar as APIs no SDK de DRM do Primetime para gerenciar todos os tipos de solicitações e como implementar a lógica comercial personalizada apoiada por um banco de dados. As regras de uso nas licenças emitidas por este servidor são controladas por meio da política associada ao conteúdo no momento do empacotamento.
* Implementação de servidor personalizado — Você também pode implementar seu próprio servidor de licenciamento com o SDK. As informações descrevem como as APIs são usadas para implementar um servidor de licenças.

