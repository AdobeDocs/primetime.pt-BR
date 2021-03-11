---
title: Sobre o Adobe Access Server para transmissão protegida
description: Sobre o Adobe Access Server para transmissão protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Sobre o Adobe Access Server para transmissão protegida{#about-adobe-access-server-for-protected-streaming}

O Adobe® Access™ Server for Protected Streaming é uma implementação do servidor de licenças baseada no SDK do Adobe Access. Este servidor emite licenças para conteúdo protegido para clientes do Adobe Access.

O Adobe Access Server for Protected Streaming oferece suporte a vários locatários, o que significa que um único servidor pode ser hospedado em nome de vários editores de conteúdo, cada um com suas próprias configurações. Além disso, o servidor suporta componentes de autorização personalizados, portanto, a lógica personalizada pode ser executada antes da emissão de uma licença.

Este servidor deve ser usado com HTTP Streaming. Como resultado, essa implementação do servidor não suporta todos os recursos disponíveis no Adobe Access. Por exemplo, o Adobe Access Server for Protected Streaming não oferece suporte a solicitações de autenticação de usuários, várias políticas, licenças vinculadas a domínio, encadeamento de licenças ou mensagens de sincronização.
