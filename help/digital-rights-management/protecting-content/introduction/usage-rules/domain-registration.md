---
title: Registro de domínio do grupo de dispositivos
description: Registro de domínio do grupo de dispositivos
copied-description: true
exl-id: 81d6023b-76e0-4786-805b-bfe77e9f8513
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Registro de domínio do grupo de dispositivos{#device-group-domain-registration}

Como alternativa à vinculação de uma licença a um dispositivo específico, o Primetime DRM 3.0 ou posterior oferece suporte à vinculação de licenças a um domínio de dispositivo.

Vários dispositivos podem ingressar em um domínio e receber tokens de domínio. Depois que um dispositivo no domínio adquirir uma licença, ela poderá ser transferida para qualquer outro dispositivo no domínio e esses dispositivos poderão reproduzir o conteúdo sem adquirir uma licença diretamente do servidor de licenças.

Se você quiser oferecer suporte a licenças vinculadas a domínio, a política DRM do Primetime deverá especificar o servidor de domínio no qual o cliente deverá se registrar. A política DRM do Primetime também deve especificar os requisitos de autenticação do servidor de domínio, se o acesso anônimo estiver habilitado ou se o servidor exigir nome de usuário/senha ou autenticação personalizada.

O registro de domínio e as licenças vinculadas a domínio são aceitos pelos clientes DRM do Primetime versão 3.0 ou posterior. Se um cliente mais antigo ou um cliente Adobe Primetime 3.0 no Flash Player solicitar uma licença para conteúdo que ofereça suporte ao registro de domínio, o servidor de licença poderá emitir uma licença que use uma política alternativa de DRM do Primetime para oferecer suporte à associação a um dispositivo específico.
