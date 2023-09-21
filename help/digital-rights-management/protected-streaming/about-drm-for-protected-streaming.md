---
description: O Adobe Primetime DRM Server para transmissão protegida é uma implementação de servidor de licença baseada no SDK DRM do Primetime. Este servidor emite licenças de conteúdo protegido para clientes DRM do Primetime.
title: Sobre o servidor DRM da Adobe Primetime para transmissão protegida
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Sobre o servidor DRM da Adobe Primetime para transmissão protegida{#about-adobe-primetime-drm-server-for-protected-streaming}

O Adobe Primetime DRM Server para transmissão protegida é uma implementação de servidor de licença baseada no SDK DRM do Primetime. Este servidor emite licenças de conteúdo protegido para clientes DRM do Primetime.

O servidor DRM do Primetime para transmissão protegida suporta vários locatários. Você pode hospedar um único servidor em nome de vários editores de conteúdo, cada um com suas próprias definições de configuração. Além disso, o servidor oferece suporte a componentes de autorização personalizados, para que você possa executar uma lógica personalizada antes da emissão de uma licença.

Este servidor deve ser usado com HTTP Streaming. Como resultado, essa implementação de servidor não é compatível com todos os recursos disponíveis no Primetime DRM. Por exemplo, ele não aceita solicitações de autenticação de usuário, várias políticas, licenças vinculadas a domínio, encadeamento de licenças ou mensagens de sincronização.

>[!NOTE]
>
>O Adobe Primetime DRM era anteriormente chamado de Adobe Access e, antes disso, Flash Access.
