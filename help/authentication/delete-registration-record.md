---
title: Excluir Registro
description: Eliminar registro reordenado
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Excluir Registro {#delete-registration-record}

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


## Descrição {#delete-record}

Exclui o registro de código reg e libera o código reg para reutilização. 

| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>Por exemplo:</br></br>&lt;reggie_fqdn>/reggie/v1/regcode/ER45RTY | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. ID do solicitante  </br>    (Componente de caminho)</br>2.  Código de registro  </br>    (Componente de caminho) | DELETE | Nenhum | 204 |

{style="table-layout:auto"}

</br>

| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| código de registro | O valor do código de registro que seria exibido no Dispositivo de transmissão (a ser inserido no fluxo de autenticação). |

{style="table-layout:auto"}

</br>

### [Voltar para Referência da API REST](/help/authentication/rest-api-reference.md)
