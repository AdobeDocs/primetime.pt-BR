---
seo-title: Registro de Domínio do Grupo de Dispositivos
title: Registro de Domínio do Grupo de Dispositivos
uuid: fd559175-2c3c-4d71-bfa1-8de9907d2b7c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Registro de Domínio do Grupo de Dispositivos{#device-group-domain-registration}

Como alternativa ao vínculo de uma licença a um dispositivo específico, o Adobe Access 3.0 e superior oferece suporte ao vínculo de licenças a um domínio de dispositivo. Vários dispositivos podem ingressar em um domínio e receber tokens de domínio. Depois que um dispositivo no domínio adquirir uma licença, ela poderá ser transferida para qualquer outro dispositivo no domínio, e esses dispositivos poderão reproduzir o conteúdo sem adquirir uma licença diretamente do servidor de licença.

Para oferecer suporte às licenças vinculadas ao domínio, a política deve especificar o servidor de domínio com o qual o cliente deve se registrar. A política também especificará os requisitos de autenticação para o servidor de domínio (se o acesso anônimo é permitido ou se o servidor requer nome de usuário/senha ou autenticação personalizada).

As licenças de registro de domínio e de domínio vinculadas são suportadas pelos clientes do Adobe Access versão 3.0 e superior. Se um cliente mais antigo ou um cliente do Adobe Access 3.0 no Flash Player solicitar uma licença para conteúdo compatível com o registro de domínio, o servidor de licença poderá emitir uma licença usando uma política alternativa que suporte o vínculo a um dispositivo específico.
