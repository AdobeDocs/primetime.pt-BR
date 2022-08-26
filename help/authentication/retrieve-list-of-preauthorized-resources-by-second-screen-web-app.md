---
title: Recuperar a lista de recursos pré-autorizados pelo aplicativo web de segunda tela
description: Recuperar a lista de recursos pré-autorizados pelo aplicativo web de segunda tela
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Recuperar a lista de recursos pré-autorizados pelo aplicativo web de segunda tela {#retrieve-list-of-preauthorized-resources-by-second-screen-web-app}

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

Uma solicitação para a autenticação da Adobe Primetime para obter a lista de recursos pré-autorizados.

Há dois conjuntos de APIs: um conjunto para o Aplicativo de transmissão ou o Serviço do programador e um conjunto para o Aplicativo Web de segunda tela. Esta página descreve a API do aplicativo AuthN.

 \
| Ponto final | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta | | — | — | — | — | — | — | | &lt;sp_fqdn>/api/v1/preauthorized/{código de registro} | Módulo AuthN | 1.  código de registro  </br>    (Componente de caminho)</br>2.  solicitante (Obrigatório)</br>3.  lista de recursos (Obrigatório) | GET | XML ou JSON contendo decisões individuais de pré-autorização ou detalhes do erro. Veja as amostras abaixo. | 200 - Êxito</br></br>400 - Solicitação incorreta</br></br>401 - Não autorizado</br></br>405 - Método não permitido  </br></br>412 - Falha na pré-condição</br></br>500 - Erro interno do servidor |



| Parâmetro de entrada | Descrição |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| código de registro | O valor do código de registro fornecido pelo usuário no início do fluxo de autenticação. |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| lista de recursos | Uma string que contém uma lista delimitada por vírgulas de resourceIds que identifica o conteúdo que pode ser acessível a um usuário e é reconhecido pelos endpoints de autorização MVPD. |


### Resposta de exemplo {#sample-response}

**XML:**

```XML
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4`
Adobe-Response-Confidence : full
Content-Type: application/xml; charset=utf-8

<resources>
    <resource>
        <id>TestStream1</id>
        <authorized>true</authorized>
    </resource>
    <resource>
        <id>TestStream2</id>
        <authorized>false</authorized>  
        <error>
            <status>403</status>
            <code>authorization_denied_by_mvpd</code>
            <message>User not authorized</message>
            <details>Your subscription package does not include the "TestStream3" channel.</details>
            <helpUrl>https://tve.helpdocsonline.com/errors/preauthorization_denied</helpUrl>
            <trace>0453f8c8-167a-4429-8784-cd32cfeaee58</trace>
            <action>none</action>
        </error>
    <resource>
</resources>
```

**JSON:**

```JSON
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
Adobe-Response-Confidence : full
Content-Type: application/json; charset=utf-8
 
{
   "resources" : [
        {
            "id" : "TestStream1",
            "authorized" : true
        },
        {
            "id" : "TestStream3",
            "authorized" : false,
            "error" : {
               "status" : 403,
               "code" : "authorization_denied_by_mvpd",
               "message" : "User not authorized",
               "details" : "Your subscription package does not include the "TestStream3" channel.",
               "helpUrl" : "https://tve.helpdocsonline.com/errors/preauthorization_denied",
               "trace" : "0453f8c8-167a-4429-8784-cd32cfeaee58",
               "action" : "none"
            }
        } 
    ]
}
```
 

### [Voltar para Referência da API REST](http://tve.helpdocsonline.com/rest-api-reference)
