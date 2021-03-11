---
description: O Adobe Primetime DRM Server for Protected Streaming é uma implementação do servidor de licenças baseada no SDK DRM do Primetime. Esse servidor emite licenças para conteúdo protegido para clientes DRM do Primetime.
title: Sobre o servidor DRM Adobe Primetime para transmissão protegida
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Sobre o servidor DRM Adobe Primetime para transmissão protegida{#about-adobe-primetime-drm-server-for-protected-streaming}

O Adobe Primetime DRM Server for Protected Streaming é uma implementação do servidor de licenças baseada no SDK DRM do Primetime. Esse servidor emite licenças para conteúdo protegido para clientes DRM do Primetime.

O Primetime DRM Server for Protected Streaming oferece suporte a vários locatários. Você pode hospedar um único servidor em nome de vários editores de conteúdo, cada um com suas próprias configurações. Além disso, o servidor suporta componentes de autorização personalizados, de modo que você pode executar a lógica personalizada antes da emissão de uma licença.

Este servidor deve ser usado com HTTP Streaming. Como resultado, essa implementação do servidor não suporta todos os recursos disponíveis no DRM do Primetime. Por exemplo, ele não suporta solicitações de autenticação de usuário, várias políticas, licenças vinculadas a domínio, cadeia de licença ou mensagens de sincronização.

>[!NOTE]
>
>O DRM da Adobe Primetime era anteriormente chamado de Adobe Access e, antes disso, Flash Access.

