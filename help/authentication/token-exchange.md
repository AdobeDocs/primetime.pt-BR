---
title: Trocar um token de SSO da plataforma por um token de Adobe
description: Trocar um token de SSO da plataforma por um token de Adobe
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 2%

---


# Trocar um token de SSO da plataforma por um token de Adobe {#exchange-a-platform-sso-token-for-an-adobe-token}

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

Permite que um perfil de SSO da plataforma seja &quot;trocado&quot; por um token de Adobe.

| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. solicitante (Obrigatório)</br>    </br>2.  deviceId (Obrigatório)</br>    </br>3.  mvpd (Obrigatório)</br>    </br>4.  deviceType (Obrigatório)</br>    </br>5.  SAMLResponse (Obrigatório)</br>    </br>6.  deviceUser (obsoleto)</br>    </br>7.  appId (obsoleto) | POST | A resposta bem-sucedida será 204 Sem conteúdo, indicando que o token foi criado com êxito e está pronto para uso para os fluxos de autenticação. | 204 - Sem conteúdo   </br>400 - Solicitação incorreta |


| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| deviceId | Os bytes da ID do dispositivo. |
| mvpd | O ID do MVPD para o qual esta operação é válida. |
| deviceType | A plataforma do Apple para a qual estamos tentando obter uma solicitação de perfil.  Ou **iOS** ou **tvOS**. |
| SAMLResponse | O perfil real como retornado pelo SSO da plataforma. |
| _deviceUser_ | O identificador do usuário do dispositivo. |
| _appId_ | A ID/nome do aplicativo. |


