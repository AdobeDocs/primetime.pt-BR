---
title: Pré-autorizar
description: Pré-autorização de JavaScript
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---

# Pré-autorizar {#js-preauthorize}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Visão geral {#preauth-overview}

O método da API pré-autorizada deve ser usado por aplicativos para obter decisões de pré-autorização para um ou mais recursos. A solicitação da API pré-autorizada deve ser usada para dicas da interface do usuário e/ou filtragem de conteúdo. Uma solicitação de API de autorização real deve ser feita antes de permitir o acesso do usuário aos recursos especificados.

Caso ocorra um erro inesperado (por exemplo, problema de rede e ponto de acesso de autorização MVPD indisponível) quando uma solicitação de API pré-autorizada for processada pelos serviços de autenticação da Adobe Primetime, uma ou várias informações de erro separadas serão incluídas para os recursos afetados como parte do resultado da resposta da API pré-autorizada.

### public preauthorize(solicitação: PreauthorizeRequest, retorno de chamada: AccessEnablerCallback&lt;any>): void {#preauth-method}

**Descrição:** Este método deve ser usado por aplicativos para obter decisões de pré-autorização do usuário autenticado (informativas) do serviço de Autenticação da Adobe Primetime para exibir recursos protegidos específicos, com o objetivo principal de decorar a interface do usuário do aplicativo (por exemplo, indicar o status de acesso com ícones de bloqueio e desbloqueio).

**Disponibilidade:** v4.4.0+

**Parâmetros:**

* `PreauthorizeRequest`: objeto Builder usado para definir a solicitação
* `AccessEnablerCallback`: retorno de chamada usado para retornar a resposta da API
* `PreauthorizeResponse`: objeto usado para retornar o conteúdo de resposta da API

### classe PreauthorizeRequestBuilder {#preath-req-builder-class}

#### setResources(resources: string[]): PreauthorizeRequestBuilder {#set-res-preath-req-buildr}

* Define a Lista de recursos para os quais você deseja obter decisões de pré-autorização.
* É obrigatório defini-lo para o uso da API pré-autorizada.
* Cada elemento na lista deve ser uma String representando o valor da ID do recurso ou o fragmento de RSS de mídia que deve ser acordado com o MVPD.
* Este método define as informações somente no contexto da atual `PreauthorizeRequestBuilder` instância do objeto, que é o receptor desta chamada de método.

* Para construir um real `PreauthorizeRequest` você pode ver `PreauthorizeRequestBuilder`Método de:

```JavaScript
  build(): PreauthorizeRequest
```

* `@param {string[]}` recursos. A Lista de recursos para os quais você deseja obter decisões de pré-autorização.
* `@returns {PreauthorizeRequestBuilder}` A referência ao mesmo `PreauthorizeRequestBuilder` instância do objeto, que é o receptor da chamada do método.
* Ela faz isso para permitir a criação de encadeamento de métodos.

#### disableFeatures(...features: string[]): PreauthorizeRequestBuilder {#disabl-featres-preauth-req-buildr}

* Define os recursos que você deseja desabilitar ao obter decisões de pré-autorização.
* Esta função define as informações somente no contexto da atual `PreauthorizeRequestBuilder` instância do objeto, que é o receptor dessa chamada de função.
* Para construir um real `PreauthorizeRequest` você pode ver `PreauthorizeRequestBuilder`função de:

```JavaScript
public func build() -> PreauthorizeRequest
```

* `@param {string[]}` recursos. O conjunto de recursos que você deseja que eles sejam desativados.
* `@returns` A referência ao mesmo `PreauthorizeRequestBuilder` instância do objeto, que é o receptor da chamada de função.
* Ele faz isso para permitir a criação de encadeamento de funções.

#### build(): PreauthorizeRequest {#preauth-req}

* Cria e recupera a referência de um novo `PreauthorizeRequest` instância do objeto.
* Este método instancia um novo `PreauthorizeRequest` sempre que é chamado.
* Este método usa os valores definidos antecipadamente no contexto de valores atuais `PreauthorizeRequestBuilder` instância do objeto, que é o receptor desta chamada de método.
* Tenha em mente que este método não produz quaisquer efeitos colaterais,
* portanto, não altera o estado do SDK nem o estado do `PreauthorizeRequestBuilder` instância do objeto, que é o receptor desta chamada de método.
* Isso significa que as chamadas sucessivas desse método para o mesmo receptor criarão novas `PreauthorizeRequest` ocorrências de objeto, mas tendo as mesmas informações, caso os valores sejam definidos como `PreauthorizeRequestBuilder` onde não foi modificado entre as chamadas.
* Caso não precise atualizar nenhuma das informações fornecidas (recursos e armazenamento em cache), é possível reutilizar a instância PreauthorizeRequest para vários usos da API pré-autorizada.
* `@returns {PreauthorizeRequest}`

### interface AccessEnablerCallback&lt;t> {#interface-access-enablr-callback}

#### onResponse(resultado: T); {#on-response-result}

* O retorno de chamada de resposta é chamado pelo SDK quando a solicitação da API pré-autorizada é atendida.
* O resultado é bem-sucedido ou um resultado de erro contendo um status.
* `@param {T} result`

#### onFailure(resultado: T); {#on-failure-result}

* Falha no retorno de chamada chamado pelo SDK quando a solicitação da API pré-autorizada não pôde ser atendida.
* O resultado é um resultado de falha contendo um status.
* `@param {T} result`

### classe PreauthorizeResponse {#preauth-response-class}

#### status público: Status; {#public-status}

* Retorna: informações adicionais de status (estado) em caso de falha.
* Pode conter um `null` valor.

#### decisões públicas: Decisão[]; {#public-decisions}

* Retorna: a lista de decisões de pré-autorização. Uma decisão para cada recurso.
* A lista pode estar vazia em caso de falha.

### Status da classe {#class-status}

#### estatuto público: número; {#public-status-numbr}

* O código de status de resposta HTTP conforme documentado na RFC 7231.
* Pode ser 0 caso a variável `Status` vem do SDK em vez dos serviços de autenticação da Adobe Primetime.

#### código público: número; {#public-code-numbr}

* O código de erro padrão dos serviços de autenticação da Adobe Primetime.
* Pode conter uma string vazia ou uma `null` valor.

#### mensagem pública: cadeia de caracteres; {#public-msg-string}

* A mensagem detalhada que, em alguns casos, é fornecida pelos endpoints de autorização do MVPD ou pelas regras de degradação do programador.
* Pode conter uma string vazia ou uma `null` valor.

#### detalhes públicos: sequência de caracteres; {#public-details-strng}

* Contém uma mensagem detalhada que, em alguns casos, é fornecida pelos endpoints de autorização do MVPD ou pelas regras de degradação do Programador.
* Pode conter uma string vazia ou uma `null` valor.


#### public helpUrl: string; {#public-help-url-string}

* O URL que vincula mais informações sobre por que esse estado/erro ocorreu e possíveis soluções.
* Pode conter uma string vazia ou uma `null` valor.

#### rastro público: cadeia de caracteres; {#public-trace-string}

* O identificador exclusivo para essa resposta, que pode ser usado ao entrar em contato com o suporte para identificar problemas específicos em cenários mais complexos.
* Pode conter uma string vazia ou uma `null` valor.

#### ação pública: sequência de caracteres; {#public-action-string}

* A ação recomendada para corrigir a situação.
   * **nenhum**: Infelizmente, não há nenhuma ação predefinida para corrigir esse problema. Isso pode indicar uma invocação incorreta da API pública
   * **configuração**: é necessária uma alteração na configuração por meio do painel TVE ou entrando em contato com o suporte.
   * **registro de aplicativos**: o aplicativo deve se registrar novamente.
   * **autenticação**: o usuário deve se autenticar ou autenticar novamente.
   * **autorização**: o usuário deve obter autorização para o recurso específico.
   * **degradação**: alguma forma de degradação deve ser aplicada.
   * **tentar novamente**: tentar novamente a solicitação pode resolver o problema
   * **tentar-depois**: tentar novamente a solicitação após o período indicado pode resolver o problema.
* Pode conter uma string vazia ou uma `null` valor.

### Decisão de classe {#class-decision}

#### public id: string; {#public-id-string}

* A ID do recurso para a qual a decisão foi obtida.

#### público autorizado: booleano; {#public-auth-boolean}

* O valor do sinalizador que indica se a decisão foi bem-sucedida ou não.

#### erro público: Status; {#public-error-status}

* Informações adicionais de status (estado) caso ocorra algum erro. Pode conter um `null` valor.

## Exemplo de implementação de cliente {#client-imp-example}

```JavaScript
let accessEnablerApi = new window.AccessEnabler.AccessEnabler("software statement");
let accessEnablerModels = window.AccessEnabler.models;



// Build request
let requestBuilder = new accessEnablerModels.PreauthorizeRequest.getBuilder();
let request = requestBuilder
    .setResources(["RES01", "RES02", "RES03"])
    .disableFeatures("LOCAL_CACHE")
    .build();



// Create callback
let callback = {
    onResponse(response) {
        // Handle onResponse
    },
    onFailure(response) {
        // Handle onFailure
    }
};

// Invoke call
accessEnablerApi.preauthorize(request, callback);
```


## Exemplos de cenário {#scenario-examples}

### Cenário 1: todos os recursos solicitados foram autorizados {#all-req-res-auth}

<table>
<thead>
  <tr>
    <th>Sinalizador de código de erro aprimorado</th>
    <th>Resposta</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>Desabilitado</td>
    <td>

```JavaScript
        {
    "decisions": [
        {
        "id": "RES01",
        "authorized": true
        },
        {
        "id": "RES02",
        "authorized": true
        },
        {
        "id": "RES03",
        "authorized": true
        }
    ]
    }    
```

</td>
  </tr>
</tbody>


### Cenário 2: alguns recursos solicitados foram autorizados. {#sm-req-res-auth}

<table>
<thead>
  <tr>
    <th>Sinalizador de código de erro aprimorado</th>
    <th>Resposta</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>Desabilitado</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;Decisions&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;authorized&quot;: true
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>Ativado</td>
    <td>

    &quot;JavaScript
    {
    &quot;Decisions&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false,
    &quot;erro&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;: &quot;O MVPD retornou uma decisão \&quot;Deny\&quot; ao solicitar pré-autorização para o recurso especificado.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;authorized&quot;: true
    },
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### Cenário 3: nenhum dos recursos solicitados foi autorizado. {#none-req-res-auth}

<table>
<thead>
  <tr>
    <th>Sinalizador de código de erro aprimorado</th>
    <th>Resposta</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>Desabilitado</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;Decisions&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;authorized&quot;: false
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>Ativado</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;Decisions&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: false,
    &quot;erro&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;: &quot;O MVPD retornou uma decisão \&quot;Deny\&quot; ao solicitar pré-autorização para o recurso especificado.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false,
    &quot;erro&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;: &quot;O MVPD retornou uma decisão \&quot;Deny\&quot; ao solicitar pré-autorização para o recurso especificado.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;authorized&quot;: false,
    &quot;erro&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;maximum_execution_time_aded&quot;,
    &quot;message&quot;: &quot;A solicitação não foi concluída no tempo máximo permitido. Tentar novamente a solicitação pode resolver o problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;retry&quot;
    }
    }
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### Cenário 4: solicitação do cliente incorreta - nenhum recurso especificado. {#bad-cl-req-no-res-sp}

<table>
<thead>
  <tr>
    <th>Sinalizador de código de erro aprimorado</th>
    <th>Resposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Desativado/Ativado</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 400,
    &quot;code&quot;: &quot;internal_error&quot;,
    &quot;message&quot;: &quot;A solicitação falhou devido a um erro interno.&quot;,
    &quot;details&quot;: &quot;O parâmetro &#39;resource&#39; da Cadeia de caracteres[] necessária não está presente&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    },
    &quot;decisões&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Cenário 5: solicitação de cliente incorreta - recursos vazios especificados. {#bad-cl-req-empt-res-sp}

<table>
<thead>
  <tr>
    <th>Sinalizador de código de erro aprimorado</th>
    <th>Resposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Desativado/Ativado</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 412,
    &quot;code&quot;: &quot;missing_resource&quot;,
    &quot;message&quot;: &quot;O parâmetro de recurso está ausente&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    },
    &quot;decisões&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Cenário 6: erro de rede. {#ntwrk-error}

<table>
<thead>
  <tr>
    <th>Sinalizador de código de erro aprimorado</th>
    <th>Resposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Ativado</td>
    <td>

    &quot;JavaScript
    {
    &quot;Decisions&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;authorized&quot;: false,
    &quot;erro&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_received_error&quot;,
    &quot;message&quot;: &quot;Ocorreu um erro de leitura ao recuperar a resposta do serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;retry&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;authorized&quot;: false,
    &quot;erro&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_received_error&quot;,
    &quot;message&quot;: &quot;Ocorreu um erro de leitura ao recuperar a resposta do serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;retry&quot;
    }
    }
    ]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Cenário 7: o fluxo de pré-autorização foi chamado sem uma sessão AuthN válida.

<table>
<thead>
  <tr>
    <th>Sinalizador de código de erro aprimorado</th>
    <th>Resposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Desativado/Ativado</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 0,
    &quot;code&quot;: &quot;authentication_session_missing&quot;,
    &quot;message&quot;: &quot;A sessão de autenticação associada a esta solicitação não pôde ser recuperada. O usuário deve se autenticar novamente com um MVPD compatível para continuar.&quot;,
    &quot;action&quot;: &quot;authentication&quot;
    },
    &quot;decisões&quot;: []
    }
    
    &quot;

</td>
  </tr>
</tbody>
</table>



### Cenário 8: o fluxo de pré-autorização foi chamado antes da chamada setRequestor ser concluída

<table>
<thead>
  <tr>
    <th>Sinalizador de código de erro aprimorado</th>
    <th>Resposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Desativado/Ativado</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 0,
    &quot;code&quot;: &quot;requestor_not_configured&quot;,
    &quot;message&quot;: &quot;O solicitante ainda não está configurado, o que é um pré-requisito para usar qualquer API diferente da API setRequestor.&quot;,
    &quot;action&quot;: &quot;retry&quot;
    },
    &quot;decisões&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>
