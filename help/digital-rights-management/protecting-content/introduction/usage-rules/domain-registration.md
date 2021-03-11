---
title: Registro de Domínio do Grupo de Dispositivos
description: Registro de Domínio do Grupo de Dispositivos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Registro de Domínio do Grupo de Dispositivos{#device-group-domain-registration}

Como alternativa a vincular uma licença a um dispositivo específico, o Primetime DRM 3.0 ou posterior suporta a vinculação de licenças a um domínio de dispositivo.

Vários dispositivos podem ingressar em um domínio e receber tokens de domínio. Depois que um dispositivo no domínio adquirir uma licença, a licença poderá ser transferida para qualquer outro dispositivo no domínio, e esses dispositivos poderão reproduzir o conteúdo sem adquirir uma licença diretamente do servidor de licença.

Se você quiser oferecer suporte a licenças vinculadas a domínio, a política de DRM do Primetime deverá especificar o servidor de domínio com o qual o cliente deverá se registrar. A política de DRM do Primetime também deve especificar os requisitos de autenticação para o servidor de domínio se o acesso anônimo está ativado ou se o servidor requer nome de usuário/senha ou autenticação personalizada.

As licenças de registro de domínio e de domínio vinculadas são suportadas pelos clientes DRM do Primetime versão 3.0 ou posterior. Se um cliente mais antigo ou um cliente Adobe Primetime 3.0 no Flash Player solicitar uma licença para conteúdo compatível com o registro de domínio, o servidor de licença poderá emitir uma licença que use uma política DRM Primetime alternativa para suportar a vinculação a um dispositivo específico.
