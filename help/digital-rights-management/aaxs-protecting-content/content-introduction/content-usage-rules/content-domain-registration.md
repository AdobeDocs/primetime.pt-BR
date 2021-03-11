---
title: Registro de Domínio do Grupo de Dispositivos
description: Registro de Domínio do Grupo de Dispositivos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Registro de Domínio do Grupo de Dispositivos{#device-group-domain-registration}

Como alternativa a vincular uma licença a um dispositivo específico, o Adobe Access 3.0 e superior oferece suporte a licenças vinculadas a um domínio de dispositivo. Vários dispositivos podem ingressar em um domínio e receber tokens de domínio. Depois que um dispositivo no domínio adquirir uma licença, a licença poderá ser transferida para qualquer outro dispositivo no domínio, e esses dispositivos poderão reproduzir o conteúdo sem adquirir uma licença diretamente do servidor de licença.

Para oferecer suporte às licenças vinculadas ao domínio, a política deve especificar o servidor de domínio com o qual o cliente deve se registrar. A política também especificará os requisitos de autenticação para o servidor de domínio (seja o acesso anônimo permitido ou se o servidor requer nome de usuário/senha ou autenticação personalizada).

As licenças de registro de domínio e de domínio vinculadas são suportadas pelos clientes do Adobe Access versão 3.0 e superior. Se um cliente mais antigo ou um cliente do Adobe Access 3.0 no Flash Player solicitar uma licença para conteúdo compatível com o registro de domínio, o servidor de licenças poderá emitir uma licença usando uma política alternativa que suporte a vinculação a um dispositivo específico.
