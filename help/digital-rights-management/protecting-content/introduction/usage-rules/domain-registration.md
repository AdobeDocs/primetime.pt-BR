---
seo-title: Registro de Domínio do Grupo de Dispositivos
title: Registro de Domínio do Grupo de Dispositivos
uuid: 221bf6c3-0568-443d-b761-64715a57ada6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Registro de Domínio do Grupo de Dispositivos{#device-group-domain-registration}

Como alternativa ao vínculo de uma licença a um dispositivo específico, o Primetime DRM 3.0 ou posterior oferece suporte ao vínculo de licenças a um domínio de dispositivo.

Vários dispositivos podem ingressar em um domínio e receber tokens de domínio. Depois que um dispositivo no domínio adquirir uma licença, ela poderá ser transferida para qualquer outro dispositivo no domínio, e esses dispositivos poderão reproduzir o conteúdo sem adquirir uma licença diretamente do servidor de licença.

Se você quiser oferecer suporte a licenças vinculadas a domínio, a política do Primetime DRM deverá especificar o servidor de domínio com o qual o cliente deve se registrar. A política DRM Primetime também deve especificar os requisitos de autenticação para o servidor de domínio se o acesso anônimo está ativado ou se o servidor requer nome de usuário/senha ou autenticação personalizada.

As licenças de registro de domínio e de domínio vinculadas são suportadas pelos clientes Primetime DRM versão 3.0 ou posterior. Se um cliente mais antigo ou um cliente Adobe Primetime 3.0 no Flash Player solicitar uma licença para conteúdo compatível com o registro de domínio, o servidor de licença poderá emitir uma licença que usa uma política Primetime DRM alternativa para suportar a vinculação a um dispositivo específico.
