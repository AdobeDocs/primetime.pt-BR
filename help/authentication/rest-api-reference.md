---
title: Referência da API REST
description: Referência da api de resest
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 4%

---


# Referência da API REST {#rest-api-reference}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Formatos de resposta {#response-formats}


>[!NOTE]
>
> As APIs fornecidas nesses serviços podem retornar respostas em XML ou JSON (para APIs que retornam uma resposta). Há 3 maneiras diferentes de especificar o formato de resposta na solicitação:
>
>* Definir cabeçalho de aceitação HTTP como `application/xml` ou `application/json`.
>* Na carga da solicitação, especifique o parâmetro `format=xml` ou `format=json`.
>* Chame o ponto de extremidade do serviço da Web com extensão `.xml` ou `.json`. Por exemplo, `/regcode.xml` ou `/regcode.json`
>
>Você pode especificar qualquer um dos métodos acima. A especificação de vários métodos com formatos conflitantes pode resultar em erros ou saídas indesejadas.

## Endpoints REST API {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Resumo dos serviços da Web {#web_srvs_summary}

A tabela abaixo lista os serviços da Web disponíveis para a abordagem sem cliente. Clique nos pontos de extremidade dos serviços da Web para obter mais informações (solicitação e resposta de amostra, parâmetros de entrada, métodos HTTP etc.)


| Sr | Ponto Final do Serviço Web | Descrição | <!--[Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration)-->. | Hospedado em | Chamado por |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode](/help/authentication/registration-code-request.md) | Retorna o código de registro gerado aleatoriamente e o URI da página de logon | 2 | Adobe  </br>Serviço de código de registro | Dispositivo inteligente |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/return-registration-record.md) | Retorna o registro do código de registro contendo o código de registro UUID, o código de registro e a ID de dispositivo com hash | 8 | Adobe  </br>Serviço de código de registro | Autenticação do Primetime |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](/help/authentication/provide-mvpd-list.md) | Retorna a lista de MVPDs configurados para o solicitante | 5 | Adobe  </br>Primetime  </br>autenticação  </br>Serviço | Logon  </br>Web  </br>Aplicativo |
| 4. | [&lt;sp_fqdn>/api/v1/authentication](/help/authentication/initiate-authentication.md) | Inicia o processo AuthN informando o evento de seleção MVPD. Cria um registro no banco de dados de autenticação, que é reconciliado quando uma resposta bem-sucedida é recebida do MVPD (Etapa 13) | 7 | Adobe  </br>Primetime  </br>autenticação  </br>Serviço | Logon  </br>Web  </br>Aplicativo |
| 5. | Cliente de Asserção SAML | Fluxo de trabalho SAML existente entre a autenticação do Primetime e o MVPD | 13 | Primetime  </br>autenticação  </br>Serviço | Autenticação do Primetime |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](/help/authentication/check-authentication-flow-by-second-screen-web-app.md) | O Aplicativo Web de Logon pode verificar se o fluxo de logon tentado foi bem-sucedido |  | Primetime  </br>autenticação   </br>Serviço | Logon   </br>Web   </br>Aplicativo |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | Obtém metadados relacionados ao token AuthN | 15 | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/delete-registration-record.md) | Exclui o registro de código reg e libera o código reg para reutilização | 16 | Adobe  </br>Serviço de código de registro | Autenticação do Primetime |
| 9. | [&lt;sp_fqdn>/api/v1/authorized](/help/authentication/initiate-authorization.md) | Obtém a resposta de autorização. | 17 | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](/help/authentication/check-authentication-token.md) | Indica se o dispositivo tem um token AuthN não expirado. |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | Retorna o token AuthN, se encontrado. |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](/help/authentication/retrieve-authorization-token.md) | Retorna o token AuthZ, se encontrado. |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](/help/authentication/obtain-short-media-token.md) | Retorna o token de mídia curta, se encontrado - igual a /api/v1/mediatoken |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](/help/authentication/obtain-short-media-token.md) | Obtém o token de mídia curta |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 15. | [&lt;sp_fqdn>/api/v1/pré-autorizar](/help/authentication/retrieve-list-of-preauthorized-resources.md) | Recupera a lista de recursos pré-autorizados |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorized/{code}](/help/authentication/retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md) | Recupera a lista de recursos pré-autorizados |  | Primetime  </br>autenticação  </br>Serviço | Logon no aplicativo da Web |
| 17. | [&lt;sp_fqdn>/api/v1/logout](/help/authentication/initiate-logout.md) | Remova os tokens AuthN e AuthZ do armazenamento |  | Primetime  </br>autenticação   </br>Serviço | Dispositivo inteligente |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](/help/authentication/user-metadata.md) | Obtém metadados do usuário após a conclusão do fluxo de autenticação | N/D | N/D | Dispositivo inteligente |
| 19. | [&lt;sp_fqdn>/api/v1/authentication/freepreview](/help/authentication/free-preview-for-temp-pass-and-promotional-temp-pass.md) | Criar um token de autenticação para o Temp Pass ou o Temp Pass Promocionais | N/D | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |


## Segurança de API REST {#security}

Todas as APIs sem cliente de autenticação do Primetime devem ser chamadas usando o protocolo HTTPS para comunicação segura. Além disso, a maioria das APIs chamadas deve conter um token de acesso fornecido pelo [Registro dinâmico de clientes](/help/authentication/dynamic-client-registration.md).

