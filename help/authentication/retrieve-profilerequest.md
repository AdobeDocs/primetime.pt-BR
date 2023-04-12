---
title: Recuperar solicitação de perfil SSO da plataforma
description: Recuperar solicitação de perfil SSO da plataforma
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Recuperar solicitação de perfil SSO da plataforma {#retrieve-platform-sso-profile-request}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Endpoints REST API {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descrição {#description}

Esse recurso produz solicitações de perfil para uma ID do solicitante e uma tupla MVPD.


| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/{requestor}/profile-requests/{mvpd} | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. solicitante (parâmetro de caminho)</br>2. mvpd (parâmetro de caminho)</br>3. deviceType (Obrigatório) | GET | O Content-Type de resposta será application/octet-stream, pois a carga real é opaca para o aplicativo cliente.</br></br>A resposta deve ser encaminhada pelo aplicativo para a plataforma</br></br>Mecanismo SSO para obter um SSO de perfil. | 200 - Sucesso   </br>400 - Solicitação incorreta |


| Parâmetro de entrada | Descrição |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| mvpd | O ID do MVPD para o qual esta operação é válida. |
| deviceType | A plataforma do Apple para a qual estamos tentando obter uma solicitação de perfil.  Ou **iOS** ou **tvOS**. |


