---
title: API de registro de cliente dinâmico
description: API de registro de cliente dinâmico
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# API de registro de cliente dinâmico {#dynamic-client-registration-api}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview}

Atualmente, há duas maneiras pelas quais a Autenticação do Primetime identifica e registra aplicativos:

* clientes baseados em navegador são registrados por meio de permissão [listagem de domínios](/help/authentication/programmer-overview.md)
* os clientes de aplicativos nativos, como aplicativos iOS e Android, são registrados por meio do mecanismo de solicitação assinado.

A autenticação da Adobe Primetime propõe um novo mecanismo de registro de aplicativos. Este mecanismo é descrito nos parágrafos seguintes.

## Mecanismo de registro do aplicativo {#appRegistrationMechanism}

### Motivos técnicos {#reasons}

O mecanismo de autenticação na autenticação da Adobe Primetime dependia de cookies de sessão, mas por causa de [Guias personalizadas do Android Chrome](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}, este objetivo já não pode ser alcançado.

Dadas estas limitações, o Adobe introduz um novo mecanismo de registro para todos os seus clientes. É baseado na RFC OAuth 2.0 e consiste nas seguintes etapas:

1. Recuperar a declaração de software do painel TVE
1. Obter credenciais de cliente
1. Obter token de acesso

### Recuperando Declaração de Software do Painel TVE {#softwareStatement}

Para cada aplicativo que você lançar, você precisa obter uma declaração de software. Todas as instruções de software são fornecidas por meio do painel TVE, depois que os aplicativos são criados. A instrução de software deve ser implantada juntamente com o aplicativo no dispositivo do usuário.

>[!IMPORTANT]
>
>Ao usar uma declaração de software, o mecanismo de id do solicitante assinado não será mais necessário.

Para obter mais detalhes sobre como criar instruções de software, visite [Registro do cliente no painel TVE](/help/authentication/dynamic-client-registration.md).

### Obter credenciais do cliente {#clientCredentials}

Depois de recuperar uma declaração de software do TVE Dashboard, é necessário registrar seu aplicativo no servidor de autorização da Adobe Primetime. Faça isso executando uma chamada /register e recuperando seu identificador de cliente exclusivo.

**Solicitação**

| Chamada HTTP |  |
|-----------|--------------------|
| caminho | /o/client/register |
| método | POST |

| campos |  |  |
|--------------------|---------------------------------------------------------------------------|-----------|
| instrução_de_software | A declaração de software criada no Painel TVE. | mandatory |
| redirect_uri | O URI que o aplicativo usa para concluir o fluxo de autenticação. | opcional |

| cabeçalhos de solicitação |  |  |
|-----------------|--------------------------------------------------------------------------------|-----------|
| Tipo de conteúdo | application/json | mandatory |
| X-Device-Info | As informações do dispositivo, conforme definido em Passando informações do dispositivo e da conexão | mandatory |
| User-Agent | O agente do usuário | mandatory |

**Resposta**

| cabeçalhos de resposta |  |  |
|------------------|------------------|-----------|
| Tipo de conteúdo | application/json | mandatory |

| campos de resposta |  |  |
|---------------------|-----------------|----------------------------|
| client_id | String | mandatory |
| client_secret | String | mandatory |
| client_id_published_at | long | mandatory |
| redirect_uris | lista de cadeias de caracteres | mandatory |
| grant_types | lista de cadeias de caracteres<br/> **valor aceite**<br/> `client_credentials`: Usado por clientes inseguros, como o Android SDK. | mandatory |
| erro | **valores aceitos**<ul><li>invalid_request</li><li>invalid_redirect_uri</li><li>invalid_software_statement</li><li>unapproved_software_statement</li></ul> | obrigatório em um fluxo de erro |


#### Resposta de erro {#error-response}

No caso de um erro, o servidor de registro responde com um código de status HTTP 400 (Solicitação incorreta) e inclui os seguintes parâmetros na resposta:

| código de status | corpo da resposta | descrição |
| --- | --- | --- |
| HTTP 400 | {&quot;erro&quot;: &quot;invalid_request&quot;} | Falta um parâmetro obrigatório na solicitação, inclui um valor de parâmetro não suportado, repete um parâmetro ou ele está malformado. |
| HTTP 400 | {&quot;erro&quot;: &quot;invalid_redirect_uri&quot;} | O redirect_uri não é permitido para este cliente com base em seu aplicativo registrado. |
| HTTP 400 | {&quot;erro&quot;: &quot;invalid_software_statement&quot;} | A instrução de software não é válida. |
| HTTP 400 | {&quot;erro&quot;: &quot;unapproved_software_statement&quot;} | O software_id não foi encontrado na configuração. |

#### Exemplo de credenciais do cliente {#client-credentials-example}

**Solicitação:**

```HTTPS
POST /o/client/register HTTP/1.1
    User-Agent: Android
    X-Device-Info: ew0KICAibW9kZWwiOiAiVFYiLA0KICAidmVuZG9yIjogIkFwcGxlIiwNCiAgIm1hbnVmYWN0dXJlciI6ICJBcHBsZSIsDQogICJvc05hbWUiOiAidHZPUyIsDQogICJvc1ZlbmRvciI6ICJBcHBsZSIsDQogICJvc1ZlcnNpb24iOiAiMTAuMiIsDQogICJicm93c2VyVmVuZG9yIjogIkFwcGxlIiwNCiAgImJyb3dzZXJOYW1lIjogIlNhZmFyaSINCn0
    Content-Type: application/json
    Accept: application/json
    Host: sp.auth.adobe.com
 {
        "software_statement": "eyJhbGciOiJSUzI1NiJ9.
    eyJzb2Z0d2FyZV9pZCI6IjROUkIxLTBYWkFCWkk5RTYtNVNNM1IiLCJjbGll
    bnRfbmFtZSI6IkV4YW1wbGUgU3RhdGVtZW50LWJhc2VkIENsaWVudCIsImNs
    aWVudF91cmkiOiJodHRwczovL2NsaWVudC5leGFtcGxlLm5ldC8ifQ.
    GHfL4QNIrQwL18BSRdE595T9jbzqa06R9BT8w409x9oIcKaZo_mt15riEXHa
    zdISUvDIZhtiyNrSHQ8K4TvqWxH6uJgcmoodZdPwmWRIEYbQDLqPNxREtYn0
    5X3AR7ia4FRjQ2ojZjk5fJqJdQ-JcfxyhK-P8BAWBd6I2LLA77IG32xtbhxY
    fHX7VhuU5ProJO8uvu3Ayv4XRhLZJY4yKfmyjiiKiPNe-Ia4SMy_d_QSWxsk
    U5XIQl5Sa2YRPMbDRXttm2TfnZM1xx70DoYi8g6czz-CPGRi4SW_S2RKHIJf
    IjoI3zTJ0Y2oe0_EJAiXbL6OyF9S5tKxDXV8JIndSA",
  "redirect_uri": "adobepass://com.programmer"  }
```

**Resposta:**

```HTTPS
HTTP/1.1 201 Created
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
    
{
 "client_id": "s6BhdRkqt3",
 "client_secret": "t7AkePiru4",
 "client_id_issued_at": 2893256800,
 "redirect_uris": [
   "app://com.programmer.adobe#sdasdsadas"],
 "grant_types": ["client_credentials"]
}
```

**Resposta do erro:**

```HTTPS
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

### Obter token de acesso {#accessToken}

Depois de recuperar o identificador de cliente exclusivo (id do cliente e segredo do cliente) para seu aplicativo, é necessário obter um token de acesso. O token de acesso é um token OAuth 2.0 obrigatório, usado para chamar as APIs de autenticação do Primetime.

>[!NOTE]
>
>Atualmente, os tokens de acesso têm 24 horas de vida.

**Solicitação**


| **Chamada HTTP** |  |
| --- | --- |
| caminho | `/o/client/token` |
| método | POST |

| **parâmetros da solicitação** |  |
| --- | --- |
| `grant_type` | Recebido no processo de registro do cliente.<br/> **Valor aceito**<br/>`client_credentials`: Usado para clientes inseguros, como o Android SDK. |
| `client_id` | Identificador de cliente obtido no processo de registro de cliente. |
| `client_secret` | Identificador de cliente obtido no processo de registro de cliente. |

**Resposta**

| campos de resposta |  |  |
| --- | --- | --- |
| `access_token` | O valor do token de acesso que você deve usar para chamar as APIs do Primetime | mandatory |
| `expires_in` | O tempo em segundos até que access_token expire | mandatory |
| `token_type` | O tipo do token **portador** | mandatory |
| `created_at` | A hora de emissão do token | mandatory |
| **cabeçalhos de resposta** |  |  |
| `Content-Type` | application/json | mandatory |

**Resposta de erro**

No caso de um erro, o servidor de autorização responde com um código de status HTTP 400 (Solicitação incorreta) e inclui os seguintes parâmetros na resposta:

| código de status | corpo da resposta | descrição |
| --- | --- | --- |
| HTTP 400 | {&quot;erro&quot;: &quot;invalid_request&quot;} | Falta um parâmetro obrigatório na solicitação, inclui um valor de parâmetro não suportado (diferente do tipo concessão), repete um parâmetro, inclui várias credenciais, utiliza mais de um mecanismo para autenticar o cliente ou está malformado. |
| HTTP 400 | {&quot;erro&quot;: &quot;invalid_client&quot;} | Falha na autenticação do cliente porque o cliente era desconhecido. O SDK DEVE se registrar novamente no servidor de autorização. |
| HTTP 400 | {&quot;erro&quot;: &quot;unauthorized_client&quot;} | O cliente autenticado não está autorizado a usar este tipo de concessão de autorização. |

#### Exemplo de token de acesso: {#obt-access-token}

**Solicitação:**

```HTTPS
POST o/client/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
    
grant_type=client_credentials&client_id=AAA&client_secret=SSS
```

**Resposta:**

```JSON
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"bearer",
  "expires_in":3600,
  "created_at":123456789
}
```

**Resposta do erro:**

```JSON
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

## Execução de solicitações de autenticação {#autheticationRequests}

Usar o token de acesso para executar o Adobe Primetime [Chamadas de API de autenticação](/help/authentication/initiate-authentication.md). Para fazer isso, o token de acesso precisa ser adicionado à solicitação da API de uma das seguintes maneiras:

* adicionando um novo parâmetro de consulta à solicitação. Esse novo parâmetro é chamado de **access_token**.

* adicionando um novo cabeçalho HTTP à solicitação: Autorização: Portador. Recomendamos que você use o cabeçalho HTTP, pois as sequências de consulta tendem a ser visíveis nos logs do servidor.

Em caso de erro, as seguintes respostas de erro poderiam ser retornadas:

| Respostas de erro |  |  |
|-----------------|-----|--------------------------------------------------------------------------------------------------------|
| invalid_request | 400 | A solicitação está malformada. |
| invalid_client | 403 | A ID do cliente não tem mais permissão para executar solicitações. Novas credenciais de cliente devem ser geradas. |
| access_denied | 401 | O access_token não é válido (expirado ou inválido). O cliente DEVE solicitar um novo access_token. |

### Como executar exemplos de solicitações de autenticação:

**Enviando token de acesso como parâmetro de solicitação:**

```HTTPS
GET adobe-services/config?access_token=<access_token>&requestor_id=... HTTP/1.1
    
Host: sp.auth.adobe.com
```

**Enviando token de acesso como cabeçalho HTTP:**

```HTTPS
POST adobe-services/sessionDevice?device_id=platformDeviceId HTTP/1.1
    
Authorization: Bearer <access_token>
    
Host: sp.auth.adobe.com
```

**Respostas de erro como corpo da resposta:**

```HTTPS
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error":"invalid_client" }
```

**Respostas de erro como parâmetros de URL:**

```HTTPS
HTTP/1.1 302 Found
    
Location: adobepass://com.programmer.adobe?error=access_denied
```
