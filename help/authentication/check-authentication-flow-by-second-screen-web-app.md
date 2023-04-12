---
title: Verificar o fluxo de autenticação por aplicação web de segunda tela
description: Verificar o fluxo de autenticação por aplicação web de segunda tela
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Verificar o fluxo de autenticação por aplicação web de segunda tela {#check-authentication-flow-by-second-screen-web-app}

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

Essa API deve ser consumida pelo aplicativo web de logon de segunda tela para confirmar que a autenticação da Adobe Primetime reconheceu o logon bem-sucedido do MVPD. Recomendamos chamar essa API antes de mostrar uma mensagem de sucesso ao usuário final que o instrui a prosseguir para o console do dispositivo para continuar com os fluxos de trabalho.


| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{código de registro} | Logon no aplicativo da Web | 1. código de registro  </br>    (Componente de caminho)</br>2.  solicitante  </br>    (Obrigatório) | GET | XML ou JSON contendo detalhes do erro, se não tiver êxito. | 200 - Sucesso   </br>403 - Proibido |

</br>

| Parâmetro de entrada | Descrição |
| ----------------- | --------------------------------------------------------------------------------------------- |
| código de registro | O valor do código de registro fornecido pelo usuário no início do fluxo de autenticação. |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |


### Resposta de exemplo (no caso de um erro) {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [Voltar para Referência da API REST](/help/authentication/rest-api-reference.md)
