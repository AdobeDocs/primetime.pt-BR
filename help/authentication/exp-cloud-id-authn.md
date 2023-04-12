---
title: Uso de Experience Cloud ID na autenticação do Primetime
description: Uso de Experience Cloud ID na autenticação do Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# Uso de Experience Cloud ID na autenticação do Primetime

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## O que é a Experience Cloud ID e como obtê-la? {#what-exp-cloud-id-obtain}

A ID do Experience Cloud (ECID para encurtar) é uma ID exclusiva gerada pelo Adobe Experience Cloud para cada usuário individual em seu aplicativo/site. A ECID é amplamente usada em todos os relatórios de Experience Cloud que estão sendo usados para vincular informações sobre um usuário específico em vários aplicativos/sites.

Se você já tiver um sistema que forneça uma ID de visitante, deverá usar a mesma ID para o escopo deste documento.

Uma maneira de obter o ECID é usar o serviço de Experience Cloud ID. Você pode usar o tipo de implementação preferido, com base no TDM, na biblioteca JS, no lado do servidor, na integração direta ou nas bibliotecas nativas para plataformas móveis. Para obter uma visão abrangente dos serviços, bibliotecas, SDKs e guias de implementação disponíveis, consulte: https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-implementation-guides.html





## Qual é o benefício de usar a Experience Cloud ID na autenticação do Primetime? {#benefit-ex-cloud-id}

Se você configurar nossos SDKs e a API REST sem cliente para usar sua ECID, poderá, posteriormente, vincular dados coletados pela autenticação do Primetime às soluções existentes do Experience Cloud. Isso permitirá compreender melhor a jornada e a experiência de seus clientes em todas as soluções fornecidas pelo Adobe.

## Como usar a Experience Cloud ID na Autenticação do Primetime? {#how-to-ex-cloud-id-authn}

Após obter a ECID (explicado acima), é necessário transmitir essas informações para nossos SDKs e nossa API REST sem cliente. Essas informações serão passadas posteriormente para nossos servidores em cada chamada de rede feita pelo SDK. O processo de configuração é diferente para cada SDK da seguinte maneira:

### JS SDK {#js-sdk}

Para JavaScript, é necessário transmitir a ECID em um mapa como o terceiro parâmetro para a chamada de setRequestor .

**Exemplo de uso:**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### SDK do iOS/tvOS {#ios-sdk}

Para o SDK do iOS/tvOS, há um método dedicado chamado setOptions.

**Exemplo de uso:**

```JavaScript
accessEnabler.setOptions(
    [
        "visitorID": "THE_ECID_VALUE"
    ]
);
```

### SDK do Android/fireTV {#android-sdk}

Para o SDK do Android/fireTV, o mecanismo é semelhante ao iOS. Apenas o nome do parâmetro é diferente. A API está documentada aqui.

**Exemplo de uso:**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### API sem cliente {#clientless-api}

Ao usar o Adobe Primetime por meio da REST API, a variável **ECID** deve ser enviado **em todas as APIs** como um parâmetro chamado **&#39;ap_vi&#39;**.

**Exemplo de uso:**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`