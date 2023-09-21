---
title: Opções de implantação do License Server
description: Opções de implantação do License Server
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Opções de implantação do License Server{#license-server-deployment-options}

É possível implantar o License Server usando uma das seguintes opções:

* Adobe Primetime DRM Server para Transmissão Protegida — Este Servidor de Licenças é otimizado para transmissão contínua. Por exemplo, você pode configurar o servidor para o HTTP Dynamic Streaming do Adobe com o DRM do Primetime. Esse servidor pode ser implantado facilmente com pouca configuração necessária e suporta vários locatários. Ele pode alcançar um alto nível de escalabilidade. Como essa implementação é otimizada para transmissão, ela não oferece suporte aos recursos completos de DRM do Primetime. Por exemplo, autenticação de nome de usuário/senha, domínios e encadeamento de licenças não são compatíveis. As regras de uso nas licenças emitidas por este servidor são controladas por meio de um arquivo de configuração do servidor, que substitui a política usada no momento do empacotamento.

  Consulte a *Guia do Adobe Primetime DRM Server para transmissão protegida* para obter mais detalhes sobre as regras de uso compatíveis com o License server.
* Servidor de Licenças de Implementação de Referência — Você pode usar essa configuração para personalizar a implementação do servidor. Este é um exemplo de implementação de servidor de licença, incluindo código-fonte, que demonstra como usar as APIs no SDK DRM do Primetime para gerenciar todos os tipos de solicitações e como implementar uma lógica de negócios personalizada com base em um banco de dados. As regras de uso nas licenças emitidas por este servidor são controladas por meio da política associada ao conteúdo no momento do empacotamento.
* Implementação de servidor personalizado — Você também pode implementar seu próprio servidor de licenciamento com o SDK. As informações descrevem como as APIs são usadas para implementar um servidor de licenças.
