---
title: Detalhes do fluxo de trabalho da política
description: Detalhes do fluxo de trabalho da política
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Fluxo de trabalho do BEES {#bees-workflow}

**Resumo:**

* **Política** - Crie uma política de reconhecimento de BEES do DRM que indique que o BEES é necessário para todo o conteúdo empacotado usando essa política.
* **Empacotamento** - Empacote o conteúdo usando a política DRM com reconhecimento de BEES.
* **Autenticação** : autentique o dispositivo cliente e use a API DRM do Primetime ou a API do Primetime para associar esse token ao DRM da Primetime Cloud. Isso fará com que o dispositivo cliente envie esse token de autenticação para o DRM do Primetime Cloud junto com todas as solicitações de licença. O Primetime Cloud DRM não processará esse token, mas o transmitirá (como um blob opaco) para o terminal BEES para processamento.
* **Licenciamento** - Solicite uma licença para seu conteúdo protegido. O dispositivo cliente anexará automaticamente o token de autenticação definido anteriormente à chamada.
* **Direito** - O Primetime Cloud DRM determinará que o conteúdo foi empacotado com uma política que requer o BEES. O Primetime Cloud DRM construirá uma solicitação JSON para enviar ao endpoint do BEES. A resposta do BEES instruirá o Primetime Cloud DRM sobre a emissão ou não de uma licença e, opcionalmente, sobre qual política de DRM usar.

## Detalhes do fluxo de trabalho da política {#policy-workflow-details}

Quando o Primetime Cloud DRM processa uma solicitação de licença, ele analisa a política DRM na solicitação para determinar se uma chamada para um serviço de direitos de back-end é necessária antes que o conteúdo possa ser exibido. Se um BEES chamar *é* necessário, o Primetime Cloud DRM criará a solicitação do BEES e analisará a política do DRM para obter um endpoint do URL do BEES especificado para a solicitação do BEES.

Aplique sua política de DRM que indica o requisito do BEES, especificando as duas propriedades personalizadas a seguir na política:

* `policy.customProp.1=bees.required=<true | false>`
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

Por exemplo, usando o Gerenciador de políticas do PRIMETIME DRM ( [!DNL AdobePolicyManager.jar]), você especificaria as duas seguintes propriedades personalizadas na [!DNL flashaccesstools.properties] arquivo de configuração:

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>Se você já estiver usando `policy.customProp.1` ou `policy.customProp.2` para outra propriedade, basta usar números exclusivos para as propriedades mais recentes.

## Detalhes do fluxo de trabalho do pacote {#package-workflow-details}

Durante o empacotamento do seu conteúdo protegido de acesso ao Adobe, você deve aplicar uma das políticas de DRM com reconhecimento de BEES ao conteúdo.

## Detalhes do fluxo de trabalho de autenticação {#authentication-workflow-details}

Para que o endpoint do BEES tome decisões de qualificação, o dispositivo cliente deve fornecer informações de autenticação. Você consegue isso usando seu próprio token de autenticação específico do cliente.

O Primetime Cloud DRM não precisa entender esse token; ele simplesmente transmite esse token para o terminal BEES. O dispositivo cliente é responsável por criar ou adquirir esse token e configurá-lo usando o `DRMManager.setAuthenticationToken()` API.

Faça o seguinte para associar esse token ao Primetime Cloud DRM para que ele seja enviado com a solicitação de licença:

Instanciar o `DRMManager` com os metadados DRM do conteúdo que foi empacotado para o DRM da Primetime Cloud.

A variável `setAuthenticationToken()` O método funciona ao associar a matriz de bytes fornecida ao URL do Servidor de licenças fornecido nos metadados de DRM usados para instanciar o `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

O token é enviado com todas as solicitações de licença até que o token seja limpo ao chamar `.setAuthenticationToken` com nulo como parâmetro.

## Detalhes do fluxo de trabalho de licença{#license-workflow-details}

Solicite uma licença do Primetime Cloud DRM chamando `mgr.loadVoucher()`.

## Detalhes de solicitação e resposta de direitos{#entitlement-request-and-response-details}

Quando o DRM da Primetime Cloud determina que o conteúdo foi empacotado com uma política DRM com reconhecimento de BEES, ele constrói a seguinte solicitação JSON para enviar ao endpoint BEES especificado na política DRM:

```
{
    "title":"Entitlement Request",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"Unique ID for this message. Used to confirm that the
                           returned response is for this particular message."
        },
        "version": {
            "type":"string",
            "description":"BEES Request Version. Currently 1."
        },
        "contentID": {
            "type":"string",
            "description":"Content ID (GUID)"
        },
        "customerSpecificAuthToken": {
            "type":"string",
            "description":"Base64-encoded authentication token. Must be set
                           explicitly by client before making the license request."
        }
    },
    "required": [
        "messageID",
        "version",
        "contentID"
    ]
}
```

Espera-se a seguinte resposta do ponto final BEES:

```
{
    "title":"Entitlement Response",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"ID of the Entitlement Request that this Response is
                           handling. Must exactly match the ID of the request
                           or this response will be rejected."
        },
        "version": {
            "type":"string",
            "description":"BEES Response Version. Currently 1."
        },
        "isAllowed": {
            "type":"boolean",
            "description":"Grant the license or not."
        },
        "policy": {
            "type":"string",
            "description":"Base64-encoded policy to enforce  If no policy is
                           provided, the policy that was packaged with the content
                           during packaging time will be used to generate the license."
        },
        "error": {
            "type":"integer",
            "description":"An error number produced by the entitlement server.
                           Will be passed to the client as the 'code' field of
                           the server error response."
        },
        "errorText": {
            "type":"string",
            "description":"Additional error information produced by the
                           entitlement server. Will be passed to the client as
                           the 'text' field of the server error response."
        }
    },
    "required": [
        "messageID",
        "version",
        "isAllowed"
    ]
}
```

O DRM da Primetime Cloud usa a resposta para determinar se deve ou não emitir uma licença para o dispositivo solicitante e se deve substituir uma nova política de DRM no processo de geração de licença. Se `isAllowed` é `true` e nenhuma política for fornecida na resposta, então a Política DRM original usada durante o tempo de empacotamento do conteúdo será usada para gerar a licença.
