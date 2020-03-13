---
seo-title: Adobe Pass e Adobe Access
title: Adobe Pass e Adobe Access
uuid: 09e75cd7-00b3-4f0f-869e-43dc4d5c3bf7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Adobe Pass e Adobe Access {#adobe-pass-and-adobe-access}

O Adobe Pass ( [](https://www.adobe.com/products/adobepass/)) fornece autenticação de usuário/dispositivo e autorização em vários provedores de conteúdo. O usuário deve ter uma assinatura de TV a cabo ou de TV por satélite válida.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

O Adobe Pass pode ser usado junto com o Adobe Access para proteger o conteúdo de mídia. Nesse cenário, o player de vídeo (SWF) pode carregar outro SWF chamado *Access Enabler*, hospedado pela Adobe Systems. O *Access Enabler* é usado para conectar-se ao serviço Adobe Pass e facilitar a integração SSO SAML com os sistemas de provedor de identidade MVPD (Multicanal Video Programming Distributor). Isso envolve redirecionar o navegador do usuário brevemente para a página de logon MVPD, depois persistir em um token AuthN e, por fim, retornar ao site de conteúdo com uma sessão AuthN em cache.

O *Access Enabler* pode facilitar autorizações de backend entre o serviço Adobe Pass e o MVPD. A MVPD mantém a lógica comercial e determina a que conteúdo o usuário tem direito. O direito é persistente em um token AuthZ adicional para esse recurso de conteúdo e é enviado de volta ao cliente.

Os tokens de autenticação e autorização são assinados usando a ID exclusiva e a chave privada do cliente Adobe Access para evitar adulterações ou falsificações. Esse token só pode ser acessado por meio do *Access Enabler*.

O player de vídeo pode acionar o processo chamando `getAuthorization` o *Access Enabler*. Quando tokens AuthN/AuthZ válidos estão presentes, o *AccessEnabler* emite um retorno de chamada para o player de vídeo que incluirá um token de mídia de curta duração para a reprodução do conteúdo do vídeo.

O Adobe Pass fornece uma biblioteca Java de validação de token de mídia que pode ser implantada em um servidor. Ao usar o servidor Flash Access para proteção de conteúdo, você pode integrar o validador de token de mídia com um plug-in do lado do servidor do Adobe Access para emitir automaticamente uma licença genérica depois de validar com êxito o token de mídia. O conteúdo é transmitido dos servidores CDN para o cliente. Para adquirir uma licença de conteúdo, o token de mídia de duração curta pode ser enviado ao servidor do Adobe Access, onde a validade do token é verificada e uma licença pode ser emitida.

O token AuthN de longa duração é usado geralmente pelo *Access Enabler* em todos os desenvolvedores de conteúdo para representar o AuthN para esse assinante MVPD. Além disso, o Adobe Access Server e o Verificador de token podem ser operados pela CDN ou por um provedor de serviços em nome do provedor de conteúdo.
