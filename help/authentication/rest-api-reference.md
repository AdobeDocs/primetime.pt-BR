---
title: Referência da API REST
description: Referência da api de resest
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 3%

---


# Referência da API REST {#rest-api-reference}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Formatos de resposta {#response-formats}


>[!NOTE]
>
> As APIs fornecidas nesses serviços podem retornar respostas em XML ou JSON (para APIs que retornam uma resposta). Há 3 maneiras diferentes de especificar o formato de resposta na solicitação:
>* Definir Cabeçalho de Aceitação HTTP como &quot;application/xml</code>&quot; ou &quot;application/json</code>&quot;
>* Na carga da solicitação, especifique o parâmetro &quot;format=xml</code>&quot; ou &quot;format=json</code>&quot;</li>
>* Chame o ponto de extremidade do serviço da Web com extensão .xml</code> ou .json</code>. Por exemplo, &quot;/regcode.xml</code>&quot; ou &quot;/regcode.json</code>&quot;
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


| Sr | Ponto Final do Serviço Web | Descrição | [Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration). | Hospedado em | Chamado por |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode](http://tve.helpdocsonline.com/registration-code-request) | Retorna o código de registro gerado aleatoriamente e o URI da página de logon | 2 | Adobe  </br>Serviço de código de registro | Dispositivo inteligente |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/return-registration-record) | Retorna o registro do código de registro contendo o código de registro UUID, o código de registro e a ID de dispositivo com hash | 8 | Adobe  </br>Serviço de código de registro | Autenticação do Primetime |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](http://tve.helpdocsonline.com/provide-mvpd-list) | Retorna a lista de MVPDs configurados para o solicitante | 5 | Adobe  </br>Primetime  </br>autenticação  </br>Serviço | Logon  </br>Web  </br>Aplicativo |
| 4. | [&lt;sp_fqdn>/api/v1/authentication](http://tve.helpdocsonline.com/initiate-authentication) | Inicia o processo AuthN informando o evento de seleção MVPD. Cria um registro no banco de dados de autenticação, que é reconciliado quando uma resposta bem-sucedida é recebida do MVPD (Etapa 13) | 7 | Adobe  </br>Primetime  </br>autenticação  </br>Serviço | Logon  </br>Web  </br>Aplicativo |
| 5. | Cliente de Asserção SAML | Fluxo de trabalho SAML existente entre a autenticação do Primetime e o MVPD | 13º | Primetime  </br>autenticação  </br>Serviço | Autenticação do Primetime |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](http://tve.helpdocsonline.com/check-authentication-flow-by-second-screen-web-app) | O Aplicativo Web de Logon pode verificar se o fluxo de logon tentado foi bem-sucedido |  | Primetime  </br>autenticação   </br>Serviço | Logon   </br>Web   </br>Aplicativo |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | Obtém metadados relacionados ao token AuthN | 15. | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/delete-registration-record) | Exclui o registro de código reg e libera o código reg para reutilização | 16º | Adobe  </br>Serviço de código de registro | Autenticação do Primetime |
| 9. | [&lt;sp_fqdn>/api/v1/authorized](http://tve.helpdocsonline.com/initiate-authorization) | Obtém a resposta de autorização. | 17º | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](http://tve.helpdocsonline.com/check-authentication-token) | Indica se o dispositivo tem um token AuthN não expirado. |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | Retorna o token AuthN, se encontrado. |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](http://tve.helpdocsonline.com/retrieve-authorization-token) | Retorna o token AuthZ, se encontrado. |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](http://tve.helpdocsonline.com/obtain-short-media-token) | Retorna o token de mídia curta, se encontrado - igual a /api/v1/mediatoken |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](http://tve.helpdocsonline.com/obtain-short-media-token) | Obtém o token de mídia curta |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 15. | [&lt;sp_fqdn>/api/v1/pré-autorizar](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources) | Recupera a lista de recursos pré-autorizados |  | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorized/{code}](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources-by-way-of-web-app) | Recupera a lista de recursos pré-autorizados |  | Primetime  </br>autenticação  </br>Serviço | Logon no aplicativo da Web |
| 17. | [&lt;sp_fqdn>/api/v1/logout](http://tve.helpdocsonline.com/logout) | Remova os tokens AuthN e AuthZ do armazenamento |  | Primetime  </br>autenticação   </br>Serviço | Dispositivo inteligente |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](http://tve.helpdocsonline.com/user-metadata-call) | Obtém metadados do usuário após a conclusão do fluxo de autenticação | N/D | N/D | Dispositivo inteligente |
| 19. | [&lt;sp_fqdn>/api/v1/authentication/freepreview](http://tve.helpdocsonline.com/free-preview-for-temp-pass-and-promotional-temp-pass) | Criar um token de autenticação para o Temp Pass ou o Temp Pass Promocionais | N/D | Primetime  </br>autenticação  </br>Serviço | Dispositivo inteligente |

{style=&quot;table-layout:auto&quot;}

## Segurança de API REST {#security}

Todas as APIs sem cliente de autenticação do Primetime devem ser chamadas usando o protocolo HTTPS para comunicação segura. Além disso, a maioria das APIs chamadas deve conter um token de acesso fornecido pelo [Registro dinâmico de clientes](http://tve.helpdocsonline.com/dynamic-client-registration).


## Informações relacionadas {#related}

* [Visão geral da REST API](http://tve.helpdocsonline.com/reset-api-overview)
* [Guia de servidor para servidor](http://tve.helpdocsonline.com/server-to-server-cookbook)
* [Guia do cliente para servidor](http://tve.helpdocsonline.com/client-to-server)
* [Evite usar &#39;&amp;&#39;reg\_code na solicitação de autenticação (Nota Técnica)](https://tve.zendesk.com/entries/23648011-Clientless-Avoid-using-reg-code-in-authenticate-request)
