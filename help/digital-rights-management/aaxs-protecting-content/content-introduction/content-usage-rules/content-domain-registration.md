---
title: Registro de domínio do grupo de dispositivos
description: Registro de domínio do grupo de dispositivos
copied-description: true
exl-id: 1f3e9d26-c185-4d12-accf-aa74a313f890
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Registro de domínio do grupo de dispositivos{#device-group-domain-registration}

Como alternativa à vinculação de uma licença a um dispositivo específico, o Adobe Access 3.0 e superior oferece suporte à vinculação de licenças a um domínio de dispositivo. Vários dispositivos podem ingressar em um domínio e receber tokens de domínio. Depois que um dispositivo no domínio adquirir uma licença, ela poderá ser transferida para qualquer outro dispositivo no domínio e esses dispositivos poderão reproduzir o conteúdo sem adquirir uma licença diretamente do servidor de licenças.

Para dar suporte às licenças vinculadas a domínio, a política deve especificar o servidor de domínio com o qual o cliente deve se registrar. A política também especificará os requisitos de autenticação do servidor de domínio (se o acesso anônimo for permitido ou se o servidor exigir nome de usuário/senha ou autenticação personalizada).

O registro de domínio e as licenças vinculadas a domínio são suportados pelos clientes Adobe Access versão 3.0 e superior. Se um cliente mais antigo ou um cliente do Adobe Access 3.0 no Flash Player solicitar uma licença para conteúdo que ofereça suporte ao registro de domínio, o servidor de licenças poderá emitir uma licença usando uma política alternativa que ofereça suporte à associação a um dispositivo específico.
