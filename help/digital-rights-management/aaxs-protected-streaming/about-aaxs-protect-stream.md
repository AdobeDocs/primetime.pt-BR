---
title: Sobre o Adobe Access Server para transmissão protegida
description: Sobre o Adobe Access Server para transmissão protegida
copied-description: true
exl-id: 69fbc99d-ee1a-4066-ae01-d61838db32a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Sobre o Adobe Access Server para transmissão protegida{#about-adobe-access-server-for-protected-streaming}

O Adobe® Access™ Server para Transmissão Protegida é uma implementação de servidor de licença baseada no SDK de Acesso ao Adobe. Este servidor emite licenças de conteúdo protegido para clientes do Adobe Access.

O Adobe Access Server para transmissão protegida oferece suporte a vários locatários, o que significa que um único servidor pode ser hospedado em nome de vários editores de conteúdo, cada um com suas próprias definições de configuração. Além disso, o servidor oferece suporte a componentes de autorização personalizados, de modo que a lógica personalizada pode ser executada antes de emitir uma licença.

Este servidor deve ser usado com HTTP Streaming. Como resultado, essa implementação de servidor não suporta todos os recursos disponíveis no Adobe Access. Por exemplo, o Adobe Access Server para transmissão protegida não é compatível com solicitações de autenticação de usuário, várias políticas, licenças vinculadas a domínio, encadeamento de licenças ou mensagens de sincronização.
