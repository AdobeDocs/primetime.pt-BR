---
seo-title: Detalhes do fluxo de trabalho da política
title: Detalhes do fluxo de trabalho da política
uuid: b355fcf6-3416-440f-9b30-a155e20f9f74
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---


# Fluxo de trabalho do BEES {#bees-workflow}

**Resumo:**

* **Política**  - Crie uma política sensível ao DRM BEES que indique que o BEES é necessário para todo o conteúdo empacotado usando esta política.
* **Empacotamento**  - agrupe o conteúdo usando a política de DRM sensível ao BEES.
* **Autenticação**  - Autentique seu dispositivo cliente e use a API DRM Primetime, ou a API Primetime, para associar esse token ao DRM da Primetime Cloud. Isso fará com que o dispositivo cliente envie esse token de autenticação para o Primetime Cloud DRM, juntamente com todas as solicitações de licença. O DRM da Primetime Cloud não processará esse token, mas passará (como um blob opaco) para o terminal BEES para processamento.
* **Licenciamento**  - solicite uma licença para seu conteúdo protegido. O dispositivo cliente anexará automaticamente o token de autenticação definido anteriormente à chamada.
* **Direito**  - o DRM da Primetime Cloud determinará que o conteúdo foi empacotado com uma política que requerBEES. O DRM da Primetime Cloud criará uma solicitação JSON para enviar ao ponto de extremidade BEES. A resposta do BEES instruirá o DRM da Primetime Cloud sobre se deve ou não emitir uma licença e, opcionalmente, qual política de DRM usar.

## Detalhes do fluxo de trabalho da política {#policy-workflow-details}

Quando o Primetime Cloud DRM processa uma solicitação de licença, ele analisa a política de DRM na solicitação para determinar se uma chamada para um serviço de direito de backend é necessária antes que o conteúdo possa ser exibido. Se uma chamada BEES *for* necessária, o DRM da Primetime Cloud criará a solicitação BEES, em seguida, analise a política de DRM para obter um ponto de extremidade de URL BEES especificado para a solicitação BEES.

Aplique sua política de DRM que indica o requisito BEES, especificando as duas seguintes propriedades personalizadas na política:

    * `policy.customProp.1=abelhas.required=&lt;true>`
    * `policy.customProp.2=abelhas.url=&lt;url to=&quot;&quot; your=&quot;&quot; BEES=&quot;&quot; endpoint=&quot;&quot;>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

Por exemplo, usando o Primetime DRM Policy Manager ( [!DNL AdobePolicyManager.jar]), você deve especificar as duas propriedades personalizadas a seguir no arquivo de configuração [!DNL flashaccesstools.properties]:

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>Se você já estiver usando `policy.customProp.1` ou `policy.customProp.2` para outra propriedade, basta usar números exclusivos para as propriedades mais recentes.

## Detalhes do fluxo de trabalho do pacote {#package-workflow-details}

Durante o empacotamento do conteúdo protegido pelo acesso ao Adobe, você deve aplicar uma de suas políticas de DRM com reconhecimento de BEES ao conteúdo.

## Detalhes do fluxo de trabalho de autenticação {#authentication-workflow-details}

Para que seu terminal BEES tome decisões de direito, o dispositivo cliente deve fornecer informações de autenticação. Isso é feito usando seu próprio token de autenticação específico do cliente.

O DRM da Primetime Cloud não precisa entender esse token; ele simplesmente passa esse token até o terminal BEES. O dispositivo cliente é responsável por criar ou adquirir esse token e defini-lo usando a API `DRMManager.setAuthenticationToken()`.

Faça o seguinte para associar esse token ao DRM da Primetime Cloud, para que seja enviado com a solicitação de licença:

Instancie o objeto `DRMManager` com os metadados DRM do conteúdo que foi empacotado para o DRM da Primetime Cloud.

O método `setAuthenticationToken()` funciona associando a matriz de bytes fornecida ao URL do License Server fornecido nos metadados do DRM usados para instanciar `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

O token é enviado com todas as solicitações de licença até que o token seja apagado, chamando `.setAuthenticationToken` com null como parâmetro.

## Detalhes do fluxo de trabalho da licença{#license-workflow-details}

Solicite uma licença do DRM da Primetime Cloud ligando para `mgr.loadVoucher()`.

## Detalhes da solicitação de direito e da resposta{#entitlement-request-and-response-details}

Quando o Primetime Cloud DRM determina que o conteúdo foi empacotado com uma política de DRM com reconhecimento de BEES, ele constrói a seguinte solicitação JSON para enviar ao ponto final BEES especificado na política de DRM:

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

A seguinte resposta é esperada do endpoint BEES:

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

O DRM da Primetime Cloud usa a resposta para determinar se deve ou não emitir uma licença para o dispositivo solicitante e se deve substituir uma nova política de DRM no processo de geração de licenças. Se `isAllowed` for `true` e nenhuma política for fornecida na resposta, a Política DRM original usada durante o tempo de empacotamento do conteúdo será usada para gerar a licença.