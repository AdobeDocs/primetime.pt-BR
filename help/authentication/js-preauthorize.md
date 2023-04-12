---
title: Pré-autorizar
description: Pré-autorização do JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# Pré-autorizar {#js-preauthorize}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#preauth-overview}

O método de API pré-autorização deve ser usado por aplicativos para obter decisões de pré-autorização para um ou mais recursos. A solicitação de pré-autorização de API deve ser usada para dicas de interface e/ou filtragem de conteúdo. Uma solicitação real da API de autorização deve ser feita antes de permitir o acesso do usuário aos recursos especificados.

No caso de um erro inesperado (por exemplo, problema de rede e ponto de extremidade de autorização MVPD indisponível) ocorrer quando uma solicitação de API pré-autorizada é processada pelos serviços de Autenticação da Adobe Primetime, uma ou várias informações de erro separadas serão incluídas para os recursos afetados como parte do resultado de resposta da API pré-autorizar.

### pré-autorização pública(solicitação: Pré-autorizarRequest, retorno de chamada: AccessEnablerCallback&lt;any>): void {#preauth-method}

**Descrição:** Esse método deve ser usado por aplicativos para obter decisões de pré-autorização (informativas) do usuário autenticado do serviço de Autenticação da Adobe Primetime para exibir recursos protegidos específicos, com o objetivo principal de decorar a interface do usuário do aplicativo (por exemplo, indicar o status de acesso com ícones de bloqueio e desbloqueio).

**Disponibilidade:** v4.4.0+

**Parâmetros:**

* `PreauthorizeRequest`: Objeto do construtor usado para definir a solicitação
* `AccessEnablerCallback`: retorno de chamada usado para retornar a resposta da API
* `PreauthorizeResponse`: Objeto usado para retornar o conteúdo da resposta da API

### classe PreauthorizedRequestBuilder {#preath-req-builder-class}

#### setResources(resources: string[]): Pré-autorizarRequestBuilder {#set-res-preath-req-buildr}

* Define a Lista de recursos para os quais você deseja obter decisões de pré-autorização.
* É obrigatório defini-lo para o uso da API pré-autorizada.
* Cada elemento na lista deve ser uma String que representa o valor da ID do recurso ou o fragmento RSS da mídia que deve ser concordado com o MVPD.
* Este método define as informações somente no contexto do `PreauthorizeRequestBuilder` instância de objeto, que é o receptor dessa chamada de método.

* Para criar um `PreauthorizeRequest` você pode dar uma olhada `PreauthorizeRequestBuilder`Método s :

```JavaScript
  build(): PreauthorizeRequest
```

* `@param {string[]}` recursos. A Lista de recursos para os quais você deseja obter decisões de pré-autorização.
* `@returns {PreauthorizeRequestBuilder}` A referência à mesma `PreauthorizeRequestBuilder` instância de objeto, que é o receptor da chamada de método.
* Ele faz isso para permitir a criação de um encadeamento de método.

#### disableFeatures(..recursos: string[]): Pré-autorizarRequestBuilder {#disabl-featres-preauth-req-buildr}

* Define os recursos que você deseja que sejam desativados ao obter decisões de pré-autorização.
* Essa função define as informações somente no contexto do `PreauthorizeRequestBuilder` instância de objeto, que é o receptor dessa chamada de função.
* Para criar um `PreauthorizeRequest` você pode dar uma olhada `PreauthorizeRequestBuilder`Função de :

```JavaScript
public func build() -> PreauthorizeRequest
```

* `@param {string[]}` recursos. O conjunto de recursos que você deseja que sejam desativados.
* `@returns` A referência à mesma `PreauthorizeRequestBuilder` instância de objeto, que é o receptor da chamada de função.
* Ele faz isso para permitir a criação de encadeamento de funções.

#### build(): Pré-autorizarSolicitação {#preauth-req}

* Cria e recupera a referência de um novo `PreauthorizeRequest` instância do objeto.
* Esse método instancia um novo `PreauthorizeRequest` sempre que for chamado.
* Esse método usa os valores definidos antecipadamente no contexto do atual `PreauthorizeRequestBuilder` instância de objeto, que é o receptor dessa chamada de método.
* Lembre-se de que este método não produz efeitos colaterais,
* portanto, não altera o estado do SDK ou o estado do `PreauthorizeRequestBuilder` instância de objeto, que é o receptor dessa chamada de método.
* Significa que chamadas sucessivas desse método para o mesmo receptor criarão novos `PreauthorizeRequest` instâncias de objeto, mas com as mesmas informações, caso os valores estejam definidos como `PreauthorizeRequestBuilder` onde não foi modificado entre as chamadas de .
* Caso não seja necessário atualizar nenhuma das informações fornecidas (recursos e armazenamento em cache), é possível reutilizar a instância PreauthorizedRequest para vários usos da API pré-autorizada.
* `@returns {PreauthorizeRequest}`

### interface AccessEnablerCallback&lt;t> {#interface-access-enablr-callback}

#### onResponse(result: T); {#on-response-result}

* Retorno de chamada de resposta chamado pelo SDK quando a solicitação da API pré-autorizada foi atendida.
* O resultado é um resultado bem-sucedido ou um erro contendo um status .
* `@param {T} result`

#### onFailure(result: T); {#on-failure-result}

* Retorno de chamada de falha chamado pelo SDK quando a solicitação de API pré-autorizada não pôde ser atendida.
* O resultado é um resultado de falha contendo um status .
* `@param {T} result`

### classe PreauthorizedResponse {#preauth-response-class}

#### Estado público: Estado; {#public-status}

* Retorna: Informações adicionais de status (estado) em caso de falha.
* Pode segurar um `null` valor.

#### decisões públicas: Decisão[]; {#public-decisions}

* Retorna: Lista das decisões de pré-autorização. Uma decisão para cada recurso.
* A lista pode estar vazia em caso de falha.

### Status da classe {#class-status}

#### Estado público: número; {#public-status-numbr}

* O código de status da resposta HTTP conforme documentado na RFC 7231.
* Pode ser 0, caso a variável `Status` vem do SDK em vez de serviços de autenticação da Adobe Primetime.

#### código público: número; {#public-code-numbr}

* O código de erro padrão dos serviços de autenticação da Adobe Primetime.
* Pode conter uma string vazia ou uma `null` valor.

#### mensagem pública: string; {#public-msg-string}

* A mensagem detalhada que, em alguns casos, é fornecida pelos endpoints de autorização do MVPD ou pelas regras de degradação do programador.
* Pode conter uma string vazia ou uma `null` valor.

#### detalhes públicos: string; {#public-details-strng}

* Retém uma mensagem detalhada que, em alguns casos, é fornecida pelos endpoints de autorização do MVPD ou pelas regras de degradação do programador.
* Pode conter uma string vazia ou uma `null` valor.


#### public helpUrl: string; {#public-help-url-string}

* O URL que vincula a mais informações sobre por que esse estado/erro ocorreu e as possíveis soluções.
* Pode conter uma string vazia ou uma `null` valor.

#### Rastreio público: string; {#public-trace-string}

* O identificador exclusivo para essa resposta, que pode ser usado ao entrar em contato com o suporte para identificar problemas específicos em cenários mais complexos.
* Pode conter uma string vazia ou uma `null` valor.

#### ação pública: string; {#public-action-string}

* A ação recomendada para corrigir a situação.
   * **nenhum**: Infelizmente, não existe qualquer ação predefinida para corrigir esta questão. Isso pode indicar uma invocação incorreta da API pública
   * **configuração**: Uma alteração na configuração é necessária por meio do painel TVE ou entrando em contato com o suporte.
   * **registro do pedido**: O pedido deve ser novamente registrado.
   * **autenticação**: O usuário deve autenticar ou autenticar novamente.
   * **autorização**: O usuário deve obter autorização para o recurso específico.
   * **degradação**: Deve ser aplicada alguma forma de degradação.
   * **tentar novamente**: Tentar novamente a solicitação pode resolver o problema
   * **repetir depois**: Tentar novamente a solicitação após o período indicado pode resolver o problema.
* Pode conter uma string vazia ou uma `null` valor.

### decisão de classe {#class-decision}

#### id pública: string; {#public-id-string}

* O ID do recurso para o qual a decisão foi obtida.

#### público autorizado: booleano; {#public-auth-boolean}

* O valor do indicador que indica se a decisão foi bem sucedida ou não.

#### erro público: Estado; {#public-error-status}

* Informações adicionais de status (estado) caso tenha ocorrido algum erro. Pode segurar um `null` valor.

## Exemplo de implementação do cliente {#client-imp-example}

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

### Cenário 1: Todos os recursos solicitados foram autorizados {#all-req-res-auth}

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


### Cenário 2: Foram autorizados alguns recursos solicitados. {#sm-req-res-auth}

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
    &quot;Decisões&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;Autorizado&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;Autorizado&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;Autorizado&quot;: true
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
    &quot;Decisões&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;Autorizado&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;Autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;: &quot;O MVPD retornou uma decisão \&quot;Negar\&quot; ao solicitar pré-autorização para o recurso especificado.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;Ação&quot;: &quot;nenhum&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;Autorizado&quot;: true
    },
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### Cenário 3: Nenhum dos recursos solicitados foi autorizado. {#none-req-res-auth}

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
    &quot;Decisões&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;Autorizado&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;Autorizado&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;Autorizado&quot;: false
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
    &quot;Decisões&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;Autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;: &quot;O MVPD retornou uma decisão \&quot;Negar\&quot; ao solicitar pré-autorização para o recurso especificado.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;Ação&quot;: &quot;nenhum&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;Autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_denied_by_mvpd&quot;,
    &quot;message&quot;: &quot;O MVPD retornou uma decisão \&quot;Negar\&quot; ao solicitar pré-autorização para o recurso especificado.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;Ação&quot;: &quot;nenhum&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;Autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;maximum_execution_time_aded&quot;,
    &quot;message&quot;: &quot;O pedido não foi concluído no prazo máximo permitido. Tentar novamente a solicitação pode resolver o problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;Ação&quot;: &quot;repetir&quot;
    }
    }
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### Cenário 4: Solicitação de cliente incorreta - nenhum recurso especificado. {#bad-cl-req-no-res-sp}

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
    &quot;detalhes&quot;: &quot;A string necessária[] parâmetro &#39;resource&#39; não está presente&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;Ação&quot;: &quot;nenhum&quot;
    },
    &quot;Decisões&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Cenário 5: Solicitação de cliente incorreta - recursos vazios especificados. {#bad-cl-req-empt-res-sp}

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
    &quot;Ação&quot;: &quot;nenhum&quot;
    },
    &quot;Decisões&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Cenário 6: Erro de rede. {#ntwrk-error}

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
    &quot;Decisões&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;Autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_receive_error&quot;,
    &quot;message&quot;: &quot;Erro de leitura ao recuperar a resposta do serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;Ação&quot;: &quot;repetir&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;Autorizado&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_receive_error&quot;,
    &quot;message&quot;: &quot;Erro de leitura ao recuperar a resposta do serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;Ação&quot;: &quot;repetir&quot;
    }
    }
    ]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Cenário 7: O fluxo pré-autorizado foi chamado sem uma sessão AuthN válida.

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
    &quot;message&quot;: &quot;Não foi possível recuperar a sessão de autenticação associada a esta solicitação. O usuário deve autenticar novamente com um MVPD suportado para continuar.&quot;,
    &quot;Ação&quot;: &quot;authentication&quot;
    },
    &quot;Decisões&quot;: []
    }
    
    &quot;

</td>
  </tr>
</tbody>
</table>



### Cenário 8: O fluxo pré-autorizado foi chamado antes da conclusão da chamada setRequestor

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
    &quot;code&quot;: &quot;requestor_not_configure&quot;,
    &quot;message&quot;: &quot;O solicitante ainda não está configurado, o que é um pré-requisito para usar qualquer API além da API setRequestor.&quot;,
    &quot;Ação&quot;: &quot;repetir&quot;
    },
    &quot;Decisões&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

