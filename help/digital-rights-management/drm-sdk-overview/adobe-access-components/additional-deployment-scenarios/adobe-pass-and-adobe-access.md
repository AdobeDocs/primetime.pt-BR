---
title: Autenticação Adobe Primetime e DRM Adobe Primetime
description: Autenticação Adobe Primetime e DRM Adobe Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Autenticação Adobe Primetime e DRM Adobe Primetime {#adobe-primetime-authentication-and-adobe-primetime-drm}

A autenticação da Adobe Primetime ( [https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/)) fornece autenticação e autorização de usuário/dispositivo em vários provedores de conteúdo. O usuário deve ter uma assinatura de TV a cabo ou de TV por satélite válida.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

A autenticação da Adobe Primetime pode ser usada junto com o DRM Adobe Primetime para proteger o conteúdo de mídia. Nesse cenário, o reprodutor de vídeo (SWF) pode carregar outro SWF chamado *Access Enabler*, que é hospedado pelo Adobe Systems. O *Access Enabler* é usado para se conectar ao serviço de autenticação da Adobe Primetime e facilitar a integração SAML SSO com os sistemas de provedor de identidade (Distribuidor de Programação de Vídeo Multicanal) do MVPD. Isso envolve redirecionar o navegador do usuário brevemente para a página de logon do MVPD, em seguida, persistir um token do AuthN e finalmente retornar ao site de conteúdo com uma sessão do AuthN em cache.

O *Access Enabler* pode facilitar as autorizações de back-end entre o serviço de autenticação da Adobe Primetime e o MVPD. O MVPD mantém a lógica de negócios e determina a que conteúdo o usuário tem direito. O direito é persistente em um token AuthZ adicional para esse recurso de conteúdo e é enviado de volta ao cliente.

Os tokens de autenticação e autorização são assinados usando a ID exclusiva e a chave privada do cliente DRM do Primetime para evitar adulterações ou falsificações. Este token só pode ser acessado por meio do *Access Enabler*.

O reprodutor de vídeo pode acionar o processo, chamando `getAuthorization` no *Ativador de Acesso*. Quando tokens AuthN/AuthZ válidos estão presentes, o *AccessEnabler* emite um retorno de chamada para o reprodutor de vídeo que incluirá um token de mídia de curta duração para a reprodução do conteúdo do vídeo.

A autenticação da Adobe Primetime fornece uma biblioteca Java do validador de token de mídia que pode ser implantada em um servidor. Ao usar o servidor DRM do Primetime para proteção de conteúdo, é possível integrar o validador de token de mídia com um plug-in do lado do servidor DRM do Primetime para emitir automaticamente uma licença genérica depois de validar com êxito o token de mídia. O conteúdo é então transmitido dos servidores CDN para o cliente. Para adquirir uma licença de conteúdo, o token de mídia de curta duração pode ser enviado ao servidor DRM do Primetime, onde a validade do token é verificada e uma licença pode ser emitida.

O token AuthN de vida longa é usado geralmente pelo *Ativador de Acesso* em todos os desenvolvedores de conteúdo para representar o AuthN desse assinante MVPD. Além disso, o Primetime DRM Server e o Token Verifier podem ser operados pela CDN ou por um provedor de serviços em nome do provedor de conteúdo.