---
title: Autenticação Adobe Primetime e DRM do Adobe Primetime
description: Autenticação Adobe Primetime e DRM do Adobe Primetime
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Autenticação Adobe Primetime e DRM do Adobe Primetime {#adobe-primetime-authentication-and-adobe-primetime-drm}

Autenticação do Adobe Primetime ( [https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/)) fornece autenticação e autorização de usuário/dispositivo em vários provedores de conteúdo. O usuário deve ter uma assinatura válida de TV a cabo ou TV via satélite.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

A autenticação do Adobe Primetime pode ser usada junto com o DRM do Adobe Primetime para proteger o conteúdo de mídia. Nesse cenário, o reprodutor de vídeo (SWF) pode carregar outro SWF chamado *Ativador de acesso*, que é hospedado pela Adobe Systems. A variável *Ativador de acesso* O é usado para se conectar ao serviço de autenticação da Adobe Primetime e facilitar a integração do SSO SAML com os sistemas do provedor de identidade do MVPD (Distribuidor de programação de vídeo multicanal). Isso envolve redirecionar o navegador do usuário brevemente para a página de logon do MVPD e, em seguida, persistir um token de Autenticação e finalmente retornar ao site de conteúdo com uma sessão de Autenticação em cache.

A variável *Ativador de acesso* O pode facilitar as autorizações de back-end entre o serviço de autenticação da Adobe Primetime e o MVPD. O MVPD mantém a lógica de negócios e determina a qual conteúdo o usuário tem direito. O direito é mantido em um token de AuthZ adicional para esse recurso de conteúdo e é enviado de volta ao cliente.

Os tokens de autenticação e autorização são assinados usando a ID exclusiva e a chave privada do cliente DRM do Primetime para evitar adulteração ou falsificação. Esse token só pode ser acessado por meio de *Ativador de acesso*.

O reprodutor de vídeo pode acionar o processo chamando `getAuthorization` no *Ativador de acesso*. Quando tokens de AuthN/AuthZ válidos estiverem presentes, a variável *AccessEnabler* O emite um retorno de chamada para o reprodutor de vídeo que incluirá um token de mídia de vida curta para reproduzir o conteúdo de vídeo.

A autenticação da Adobe Primetime fornece uma biblioteca Java do validador de token de mídia que pode ser implantada em um servidor. Ao usar o servidor DRM do Primetime para proteção de conteúdo, você pode integrar o validador de token de mídia a um plug-in do lado do servidor DRM do Primetime para emitir automaticamente uma licença genérica após validar com êxito o token de mídia. Em seguida, o conteúdo é transmitido dos servidores CDN para o cliente. Para adquirir uma licença de conteúdo, o token de mídia de vida curta pode ser enviado ao servidor DRM do Primetime, onde a validade do token é verificada e uma licença pode ser emitida.

O token de AuthN de vida longa é usado geralmente pelo *Ativador de acesso* em todos os desenvolvedores de conteúdo para representar o AuthN desse assinante do MVPD. Além disso, o servidor DRM do Primetime e o verificador de token podem ser operados pela CDN ou por um provedor de serviços em nome do provedor de conteúdo.
