---
title: Uso da ID de Experience Cloud na autenticação do Primetime
description: Uso da ID de Experience Cloud na autenticação do Primetime
exl-id: 03354c01-5aad-4d81-beee-1c3834599134
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Uso da ID de Experience Cloud na autenticação do Primetime

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## O que é ID de Experience Cloud e como obtê-la? {#what-exp-cloud-id-obtain}

A ID do Experience Cloud (ECID) é uma ID exclusiva gerada pelo Adobe Experience Cloud para cada usuário individual em seu aplicativo/site. A ECID é muito usada em todos os relatórios de Experience Cloud usados para vincular informações sobre um usuário específico em vários aplicativos/sites.

Se você já tiver um sistema em vigor que forneça uma ID de visitante, use a mesma ID para o escopo deste documento.

Uma maneira de obter a ECID é usar o Serviço de ID de Experience Cloud. Você pode usar seu tipo de implementação preferido, com base no TDM, biblioteca JS, no lado do servidor, integração direta ou bibliotecas nativas para plataformas móveis. Para obter uma visualização abrangente dos serviços, bibliotecas, SDKs e guias de implementação disponíveis, consulte: https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-implementation-guides.html





## Qual é o benefício de usar a ID de Experience Cloud na autenticação do Primetime? {#benefit-ex-cloud-id}

Se você configurar nossos SDKs e a API REST sem cliente para usar sua ECID, será possível vincular os dados coletados pela Autenticação do Primetime às soluções de Experience Cloud existentes. Isso permitirá que você entenda melhor a jornada e a experiência de seus clientes em todas as soluções fornecidas pela Adobe.

## Como usar a ID de Experience Cloud na autenticação do Primetime? {#how-to-ex-cloud-id-authn}

Depois de obter a ECID (explicada acima), é necessário transmitir essas informações para nossos SDKs e nossa API REST sem clientes. Essas informações serão posteriormente passadas para nossos servidores em cada chamada de rede feita pelo SDK. O processo de configuração é diferente para cada SDK, da seguinte maneira:

### JS SDK {#js-sdk}

Para JavaScript, você precisa passar a ECID em um mapa como o terceiro parâmetro para a chamada setRequestor.

**Exemplo de uso:**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### iOS/tvOS SDK {#ios-sdk}

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

Para o Android/fireTV SDK, o mecanismo é semelhante ao iOS. Apenas o nome do parâmetro é diferente. A API está documentada aqui.

**Exemplo de uso:**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### API sem cliente {#clientless-api}

Ao usar o Adobe Primetime por meio da REST API, a variável **ECID** o valor deve ser enviado **em todas as APIs** como um parâmetro chamado **&#39;ap_vi&#39;**.

**Exemplo de uso:**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`
