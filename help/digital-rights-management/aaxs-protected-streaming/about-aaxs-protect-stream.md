---
title: Sobre o Adobe Access Server para transmissão protegida
description: Sobre o Adobe Access Server para transmissão protegida
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Sobre o Adobe Access Server para transmissão protegida{#about-adobe-access-server-for-protected-streaming}

O Adobe® Access™ Server para Transmissão Protegida é uma implementação de servidor de licença baseada no SDK de Acesso ao Adobe. Este servidor emite licenças de conteúdo protegido para clientes do Adobe Access.

O Adobe Access Server para transmissão protegida oferece suporte a vários locatários, o que significa que um único servidor pode ser hospedado em nome de vários editores de conteúdo, cada um com suas próprias definições de configuração. Além disso, o servidor oferece suporte a componentes de autorização personalizados, de modo que a lógica personalizada pode ser executada antes de emitir uma licença.

Este servidor deve ser usado com HTTP Streaming. Como resultado, essa implementação de servidor não suporta todos os recursos disponíveis no Adobe Access. Por exemplo, o Adobe Access Server para transmissão protegida não é compatível com solicitações de autenticação de usuário, várias políticas, licenças vinculadas a domínio, encadeamento de licenças ou mensagens de sincronização.
