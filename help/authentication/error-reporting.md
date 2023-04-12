---
title: Relatório de erros
description: Relatório de erros
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# Relatório de erros {#error-reporting}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Visão geral {#overview}

O relatório de erros na Autenticação do Adobe Primetime está implementado de duas maneiras diferentes no momento:

* **Relatório de erros avançados** O implementador registra um retorno de chamada de erro no caso da variável [SDK do JavaScript do AccessEnabler](#accessenabler-javascript-sdk) ou implementa um método da interface chamado &quot;`status`&quot; no caso de [SDK do AccessEnabler iOS/tvOS](#accessenabler-ios-tvos-sdk) e [SDK do Android do AccessEnabler](#accessenabler-android-sdk)para receber relatórios de erros avançados. Os erros são categorizados em **Informações**, **Aviso** e **Erro** tipos. Este sistema de informação é **assíncrono**, na medida em que **não há garantia da ordem em que vários erros serão acionados**.  Para obter detalhes sobre o sistema avançado de relatório de erros, consulte [Relatório de erros avançados](#advanced-error-reporting) seção.

* **Relatório de erro original -** Um sistema de relatórios estático no qual as mensagens de erro são passadas para funções de retorno de chamada específicas quando solicitações específicas falham. Os erros são agrupados em tipos genéricos, de autenticação e de autorização. Para obter a lista de erros relatados no sistema original, consulte o [Relatório de erro original](#original-error-reporting) seção.


## Relatório de erros avançados {#advanced-error-reporting}

* [SDK do JavaScript do AccessEnabler](#accessenabler-javascript-sdk)
* [SDK do AccessEnabler iOS/tvOS](#accessenabler-ios-tvos-sdk)
* [SDK do Android do AccessEnabler](#accessenabler-android-sdk)
* [SDK do AccessEnabler FireOS](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>O velho [Relatório de erro original](#original-error-reporting) A API continuará a funcionar da mesma maneira que antes, o relatório avançado de erros não interrompe a funcionalidade, mas o relatório original de erros NÃO receberá mais atualizações. Todos os novos erros e atualizações ocorrerão no sistema avançado de relatório de erros.

### SDK do JavaScript do AccessEnabler {#accessenabler-javascript-sdk}

O novo sistema de relatório de erros é opcional, portanto, o implementador pode registrar explicitamente um retorno de chamada do manipulador de erros para receber relatórios de erros avançados. O sistema inclui a capacidade de registrar e cancelar o registro de vários retornos de chamada de erro dinamicamente. Além disso, você pode registrar qualquer novo retorno de chamada de erro assim que o SDK do JavaScript do AccessEnabler for carregado, sem a necessidade de executar qualquer outra inicialização (antes de chamar `setRequestor()`), o que significa que você pode receber relatórios avançados sobre erros de inicialização e configuração.


#### Implementação {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


Sua função de retorno de chamada do manipulador de erros receberá um único objeto (um mapa) com a seguinte estrutura:

```JavaScript
    {
      errorId: "CFG410",
      level: "error",
      message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

### 1. Ligação {#bind}

**`.bind(eventType:String, handlerName:String):void`**

Anexa um manipulador para um evento.

**`eventType`** - SOMENTE o &quot;`errorEvent`&quot; resulta no SDK do JavaScript do AccessEnabler acionando retornos de chamada de relatórios de erro avançados.

**`handlerName`** - uma string que especifica o nome da função do manipulador de erros.\
 

Ambos os parâmetros de vínculo devem usar somente caracteres do seguinte conjunto: `[0-9a-zA-Z][-._a-zA-Z0-9]`; ou seja, os parâmetros devem começar com um número ou letra e podem incluir somente hifens, pontos, sublinhados e caracteres alfanuméricos.  Além disso, os parâmetros não podem exceder 1024 caracteres.  

**Exemplo** de manipuladores de erro de vínculo:

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

Devido a limitações técnicas, não é possível vincular um fechamento ou uma função anônima. Você deve especificar o nome do método no segundo parâmetro.

 
### 2. Desvincular {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

Remove um manipulador de eventos anexado anteriormente.

**`eventType`** - SOMENTE o &quot;`errorEvent`O valor &#39; resulta no SDK do JavaScript do AccessEnabler acionando retornos de chamada de relatórios de erro avançados.

**`handlerName`** - uma string que especifica o nome da função do manipulador de erros, se for nula ou estiver faltando todos os manipuladores anexados para o `eventType` serão removidas.

Ambos os parâmetros de vínculo devem usar somente caracteres do seguinte conjunto: `[0-9a-zA-Z][-._a-zA-Z0-9]`; ou seja, os parâmetros devem começar com um número ou letra e podem incluir somente hifens, pontos, sublinhados e caracteres alfanuméricos.  Além disso, os parâmetros não podem exceder 1024 caracteres.  

**Exemplo** da remoção de um único manipulador de erros:

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**Exemplo** removendo todos os manipuladores de erro:

`accessEnabler.unbind('errorEvent');`


### SDK do AccessEnabler iOS/tvOS {#accessenabler-ios-tvos-sdk}

O novo sistema de relatório de erros é obrigatório, portanto, o implementador deve estar em conformidade explicitamente com o novo protocolo Objetive C &quot;EntitlementStatus&quot; . Essa nova abordagem permite que os programadores recebam relatórios de erros avançados.

#### Implementação {#accessenab-ios-tvossdk-imp}

Um implementador precisa estar em conformidade com o seguinte **EntitlementStatus** protocolo:

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

Seu **status** receberá um único objeto (um `NSDictionary`) com a seguinte estrutura:

```OBJ-C
    {
          errorId: "CFG410",
          level: "error",
          message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

**1. Declaração**

```OBJ-C
    @interface MyEntitlementStatusDelegate : NSObject <EntitlementStatus>
```

**2. Implementação**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### SDK do Android do AccessEnabler {#accessenabler-android-sdk}

O novo sistema de relatório de erros é obrigatório, pois o implementador deve estar em conformidade com `IAccessEnablerDelegate` protocolo definido pela interface. Essa nova abordagem permite que os programadores recebam relatórios de erros avançados.

#### Implementação {#access-enablr-androidsdk-imp}

Um implementador precisa lidar com o novo `status` método da interface`IAccessEnablerDelegate`. O **`status`** receberá uma única **`AdvancedStatus`** objeto com o seguinte modelo:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Amostra**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

### SDK do AccessEnabler FireOS {#accessenabler-fireos-sdk}


O novo sistema de relatório de erros é obrigatório, pois o implementador deve estar em conformidade com `IAccessEnablerDelegate` protocolo definido pela interface. Essa nova abordagem permite que os programadores recebam relatórios de erros avançados.

#### Implementação {#access-enab-fireos-sdk-}

Um implementador precisa lidar com o novo `status`método da interface`IAccessEnablerDelegate`. O **`status`** receberá uma única **`AdvancedStatus`** objeto com o seguinte modelo:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Amostra**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

## Referência de códigos de erro avançados {#advanced-error-codes-reference}

A tabela a seguir lista e descreve os códigos de erro expostos pela API de erro mais recente, juntamente com as ações sugeridas a serem tomadas para corrigi-los:

| ID | Nível | Descrição | Ações do desenvolvedor | Ações do usuário | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL &amp; AAPL_ERROR | Erro | Erro de Apple SSO genérico | O erro contém um campo de detalhes com o erro VSA original. | n/d | n/d | Sim | n/d |
| VSA203 | Informações | O usuário decidiu sair do aplicativo enquanto a autenticação ocorria como resultado de um logon por meio do SSO da plataforma. | Instrua/solicite ao usuário que saia explicitamente de Configurações -> Contas -> Provedor de TV no tvOS. <br><br> Instrua/solicite que o usuário saia explicitamente de Configurações -> Provedor de TV no iOS/iPadOS. | Faça logoff explicitamente em Configurações -> Contas -> Provedor de TV no tvOS. <br> <br> Fazer logoff explicitamente em Configurações -> Provedor de TV no iOS/iPadOS | n/d | Sim | n/d |
| VSA404 | Informações | A permissão de Conta de Assinante de Vídeo do Aplicativo é indeterminada. | Incentize usuários que se recusam a conceder permissão de acesso às informações de assinatura explicando os benefícios da experiência de usuário de Logon único (SSO). | O usuário pode alterar sua decisão acessando as configurações do aplicativo (acesso do Provedor de TV) ou a seção de Configurações -> Provedor de TV em iOS/iPadOS ou Configurações -> Contas -> Provedor de TV em tvOS. | n/d | Sim | n/d |
| VSA503 | Informações | Falha na solicitação de metadados da Conta do Assinante de Vídeo do Aplicativo. | O ponto de extremidade MVPD não está respondendo. O aplicativo pode fallback para o fluxo de autenticação regular. | n/d | n/d | Sim | n/d |
| 500 | Erro | Erro interno | Use AccessEnablerDebug e inspecione os logs de depuração (saída do console.log) para determinar o que deu errado. | n/d | Sim | Sim | n/d |
| SEC403 | Erro | Erro de segurança de domínio. O solicitante está usando um domínio inválido. Todos os domínios usados por uma ID de solicitante específica precisam estar na lista de permissões do Adobe. | - Carregar o AccessEnabler somente a partir da lista de domínios permitidos <br> <br> - Entre em contato com o Adobe para gerenciar a lista de permissões do domínio para a ID do solicitante usada <br> <br> - iOS: verifique se você está usando o certificado correto e se a assinatura foi criada corretamente | n/d | n/d | Sim | n/d |
| SEC412 | Aviso | [ Disponível na versão 2.5 ] A ID do dispositivo não corresponde. Isso pode acontecer sempre que a plataforma subjacente alterar a ID do dispositivo. Nesse caso, os tokens existentes serão limpos e o usuário não será mais autenticado. Observe que isso ocorre legitimamente quando o usuário está usando o JS SDK e está em roaming (no JS, o IP do cliente faz parte da ID do dispositivo). Caso contrário, isso pode ser uma indicação de uma tentativa de fraude - uma tentativa de copiar tokens de um dispositivo diferente. | - Monitore o número de avisos. Se picos sem motivo aparente (nenhum navegador recente é atualizado); novos sistemas operacionais) que podem ser um indicador de tentativas de fraude.  <br> <br>- Opcionalmente, informe o usuário de que ele precisa fazer logon novamente. | Faça logon novamente. | Sim | Sim | Sim a partir de 3.2 |
| SEC420 | Erro | Erro de segurança HTTP ao se comunicar com os servidores de autenticação da Adobe Primetime. Normalmente, esse erro ocorre quando a falsificação/proxies está no lugar. | - Carregar `[https://]{SP_FQDN\}` no navegador e aceitar manualmente os certificados SSL, por exemplo, **https://api.auth.adobe.com** ou **https://api.auth-staging.adobe.com** <br> <br>- Marcar os certificados de proxy como confiáveis | Se isso ocorrer para um usuário regular, é uma indicação de um possível ataque homem a meio! | Sim | Sim | Sim a partir de 3.2 |
| CFG100 | Aviso | A data/hora/fuso horário da máquina cliente não está definida corretamente. Isso provavelmente levará a erros de autenticação/autorização. | - Informe o usuário para definir a hora correta. <br> <br> Execute ações para evitar fluxos de direito, pois eles provavelmente falharão. | Defina a Data/hora corretas. | Sim | Sim | Sim a partir de 3.2 |
| CFG400 | Erro | Uma ID de Solicitante inválida foi fornecida. | O desenvolvedor DEVE especificar uma ID de Solicitante válida. | n/d | Sim | Sim | Sim a partir de 3.2 |
| CFG404 | Erro | Os servidores de autenticação da Adobe Primetime não foram encontrados. Isso pode acontecer em 3 instâncias: <br><br> - O desenvolvedor tem uma falsificação inválida em vigor. <br><br> -O usuário tem problemas de rede e não pode acessar os domínios de autenticação da Adobe Primetime. <br><br> -Os servidores de autenticação da Adobe Primetime estão configurados incorretamente. <br><br>  **Observação:** No Firefox, o CFG400 será exibido em vez do CFG404 (limitação do navegador) | - Verifique a falsificação. <br><br> -Verifique as configurações de rede / DNS. <br><br> -Informe o Adobe. | Verifique as configurações de rede/DNS. | Sim | Sim | Sim a partir de 3.2 |
| CFG410 | Erro | AccessEnabler é muito antigo. | Informe o usuário para limpar os caches. | Limpe o cache do navegador. | Sim | n/d | Sim a partir de 3.2 |
| CFG5xx | Erro | Os servidores de autenticação da Adobe Primetime estão apresentando erros internos. xx pode ser qualquer número. | - Informe ao usuário a indisponibilidade da autenticação da Adobe Primetime. <br><br> - Ignorar a autenticação da Adobe Primetime. <br> <br> - Informe o Adobe. | Tente mais tarde. | Sim | Sim | Sim a partir de 3.2 |
| N000 | Informações | O usuário não está autenticado. | n/d | Logon. | Sim | Sim | Sim a partir de 3.2 |
| N001 | Informações | Uma tentativa de autenticação passiva foi iniciada em segundo plano. Isso acontecerá com os MVPDs configurados com &quot;Autenticação por Solicitante&quot;. Embora o usuário possa ser autenticado automaticamente, isso incorre em uma penalidade de desempenho na inicialização. | Opcionalmente, informe o usuário ou apresente a interface que alerta o usuário de que &quot;o trabalho está em andamento&quot;. | Espera. | Sim | Sim | Sim a partir de 3.2 |
| N003 | Informações | O usuário seleciona a opção &quot;Outro provedor de TV&quot; no seletor MVPD da Apple. | O *displayProviderDialog* o retorno de chamada será chamado e o aplicativo poderá fallback para o fluxo de autenticação regular. | Selecione MVPD regular e continue com a tela de logon. | n/d | Sim | n/d |
| N004 | Informações | O usuário seleciona um Provedor de TV que não é suportado pelo solicitante atual. | O *displayProviderDialog* o retorno de chamada será chamado e o aplicativo poderá fallback para o fluxo de autenticação regular. | Selecione MVPD regular e continue com a tela de logon. | n/d | Sim | n/d |
| N005 | Informações | O seletor de MVPD foi cancelado. | n/d | n/d | Sim | Sim | Sim a partir de 3.2 |
| N010 | Aviso | O usuário foi autenticado enquanto a regra de degradação autenticar-tudo estava em vigor para o MVPD selecionado. | Opcionalmente, informe o usuário de que ele está obtendo acesso gratuito &quot;gratuito&quot; devido a dificuldades de MVPD. | n/d | Sim | Sim | Sim a partir de 3.2 |
| N011 | Informações | O usuário foi autenticado usando o TempPass. | - Informe o usuário. <br> <br> - Apresentar opcionalmente uma lista de MVPDs regulares. | Opcionalmente, faça logon com seu MVPD normal. | Sim | Sim | Sim a partir de 3.2 |
| N111 | Aviso | TempPass expirado. | - Informe o usuário. <br> <br> - Apresentar uma lista de MVPDs regulares. <br> <br> - Ocultar a opção TempPass. | Faça logon com seu MVPD normal. | Sim | Sim | Sim a partir de 3.2 |
| N130 | Erro | **Token de autenticação não encontrado na sessão.**  Isso pode ser devido a um dos seguintes motivos: <br> <br> 1. O navegador tem cookies (de terceiros) desativados (Não aplicável para o SDK do JavaScript do AccessEnabler versão 4.x) <br> <br> 2. O navegador impediu o rastreamento entre sites ativado (Safari 11+) <br> <br> 3. A sessão expirou <br> <br> 4. Programador chama APIs de autenticação na sucessão incorreta <br> <br> OBSERVAÇÃO: Esse código de erro não está disponível para fluxos de autenticação de redirecionamento de página inteira. | 1. Solicitar que o usuário ative cookies (de terceiros) <br> <br> 2. Solicitar que o usuário desative o rastreamento entre sites <br> <br> 3. Solicitar que o usuário reautentique <br> <br> 4. Chame as APIs na ordem correta | 1. Ativar cookies (de terceiros) <br> <br> 2. Desativar o rastreamento entre sites <br> <br> 3. Reautenticar <br> <br> 4. N/D | Sim | Sim | Sim a partir de 3.2 |
| N500 | Erro | Erro interno. <br> <br> Observação: Este é o &quot;Erro de autenticação genérico&quot; e &quot;Erro de autenticação interna&quot; do sistema de erro original. Esse erro será eliminado gradualmente. | Use AccessEnablerDebug e inspecione os logs de depuração (saída do console.log) para determinar o que deu errado. | n/d | Sim | Sim | n/d |
| R401 | Erro | Erro ao tentar obter um token de acesso. <br> <br> Observação: Este é um erro irrecuperável. Informe ao usuário que o aplicativo está indisponível. | - iOS: Verifique a declaração de software e os esquemas personalizados em seu aplicativo. <br> <br> - JavaScript: Verifique a instrução do software no aplicativo do site. <br> <br> Abra um tíquete usando o Zendesk e informe o usuário de que o sistema está temporariamente indisponível | n/d | Sim da v4.0 | Sim da v3.0 | Sim a partir de 3.2 |
| R400 | Erro | O aplicativo não está registrado. A declaração de software é inválida ou foi revogada. <br> <br> Observação: Este é um erro irrecuperável. Informe ao usuário que o aplicativo está indisponível. | - iOS: Verifique a declaração de software e os esquemas personalizados em seu aplicativo. <br> <br> - JavaScript: Verifique a instrução do software no aplicativo do site. <br> <br> Abra um tíquete usando o Zendesk e informe o usuário de que o sistema está temporariamente indisponível | n/d | Sim da v4.0 | Sim da v3.0 | Sim a partir de 3.2 |
| REG500 | Erro | Não foi possível obter o código de registro do servidor. <br> <br> Observação: Este é um erro irrecuperável. Informe ao usuário que o aplicativo está indisponível. | Abra um tíquete usando o Zendesk e informe o usuário de que o sistema está temporariamente indisponível. | n/d | Sim da v4.0 | Sim da v3.0 | Sim a partir de 3.2 |
| REGCODE | Sucesso | O aplicativo chamou a API setSeletedProvider na plataforma tvOS. | Instrua/solicite ao usuário que use um segundo dispositivo (tela) para fazer logon usando o código de registro fornecido. | Use o regcode em um segundo dispositivo (tela) para iniciar a autenticação. | n/d | Sim somente para tvOS | n/d |
| Z010 | Aviso | O usuário foi autorizado enquanto a regra de degradação autenticar tudo ou autorizar tudo estava em vigor para o MVPD selecionado. | Opcionalmente, informe o usuário de que ele está obtendo acesso gratuito &quot;gratuito&quot; devido a dificuldades de MVPD. | n/d | Sim | Sim | Sim a partir de 3.2 |
| Z011 | Informações | O usuário foi autorizado usando o TempPass | Opcionalmente, informe o usuário | n/d | Sim | Sim | Sim a partir de 3.2 |
| Z100 | Erro | A autorização falhou porque o usuário não tem assinatura para o recurso solicitado ou por outros motivos originados do MVPD, por exemplo, o vídeo não corresponde às configurações de Controle dos Pais da conta de usuário | - Não permita reprodução. <br> <br> - Informe o usuário. <br> <br> - A chave &#39;message&#39; na mensagem de erro PODE conter uma mensagem mais detalhada fornecida pelo MVPD. | n/d | Sim | Sim | Sim a partir de 3.2 |
| Z110 | Erro | Autorização negada devido a recusas repetidas de MVPD. Possível tentativa de fraude ou DOS. | - Não permita reprodução. <br> <br> - Informe o usuário. | n/d | Sim | Sim | Sim a partir de 3.2 |
| Z120 | Erro | Autorização negada por motivos técnicos na comunicação com o MVPD. Possível erro de rede. | - Não permita reprodução. <br> <br> - Informe o utilizador de que o MVPD teve dificuldades e que deverá tentar mais tarde. | Tente mais tarde. | Sim | Sim | Sim a partir de 3.2 |
| Z130 | Erro | Autorização negada porque foi utilizado um recurso inválido/malformado. | Verifique a string do recurso e corrija-a. Geralmente, esse erro é devido a um MRSS malformado ou ao uso de uma string simples em vez de MRSS. | n/d | Sim | Sim | Sim a partir de 3.2 |
| Z169 | Erro | Autorização negada porque a regra de degradação authzNone foi aplicada ao recurso especificado. | Informar o usuário | n/d | Sim | Sim | Sim a partir de 3.2 |
| Z500 | Erro | Erro interno. <br> <br>  Observação: este é o &quot;Erro de autenticação genérico&quot; e &quot;Erro de autenticação interna&quot; herdados. Esse erro será eliminado gradualmente. | Use AccessEnablerDebug e inspecione os logs de depuração (saída do console.log) para determinar o que deu errado. | n/d | Sim | Sim | Sim a partir de 3.2 |
| P100 | Erro | Falha na pré-autorização. Provavelmente, isso se deve à solicitação de autorização para muitos recursos. | - NÃO use mais do que o número máximo de recursos permitidos. <br> <br> - Entre em contato com o suporte de autenticação da Adobe Primetime para encontrar/configurar o número máximo de recursos permitidos. | n/d | Sim da v3.0 | Sim | Sim a partir de 3.2 |
| IS2XX | Erro | Esses códigos de erro são retornados quando os dados de resposta do ponto de extremidade do servidor de individualização têm um formato inválido ou estão faltando informações de individualização necessárias. | Abra um tíquete usando o Zendesk e informe o usuário de que o sistema está temporariamente indisponível | n/d | Sim da v3.0 | n/d | n/d |
| IS4XX | Erro | Esses códigos de erro são retornados no caso de falha de ponto de extremidade do servidor de individualização 4XX - é o código de status HTTP da resposta. | Abra um tíquete usando o Zendesk e informe o usuário de que o sistema está temporariamente indisponível | n/d | Sim da v3.0 | n/d | n/d |
| IS5XX | Erro | Esses códigos de erro são retornados no caso de falha de ponto de extremidade do servidor de individualização 5XX - é o código de status HTTP da resposta. | Abra um tíquete usando o Zendesk e informe o usuário de que o sistema está temporariamente indisponível | n/d | Sim da v3.0 | n/d | n/d |
| IS0 | Erro | Esse código é retornado quando o ponto de extremidade do servidor de individualização não respondeu de forma alguma, portanto, a conexão expirou | Abra um tíquete usando o Zendesk e informe o usuário de que o sistema está temporariamente indisponível | n/d | Sim da v3.0 | n/d | n/d |
| LS011 | Aviso | O AccessEnabler está usando um armazenamento volátil porque devido a problemas de LSO / LocalStorage e problemas de WebStorage (ou indisponibilidade). <br> <br> A autenticação/autorização não persiste além da página atual!. Cada carregamento de página resultará na necessidade de autenticação do usuário. Os TTLs configurados não são aplicados em recarregamentos de página. | - Informe o usuário sobre as limitações. <br> <br> - Informe o usuário sobre como aumentar o espaço de armazenamento disponível. <br> <br> - Como alternativa, desconecte-se para limpar o armazenamento. | - Aumente o armazenamento. <br> <br> - Faça logoff para limpar o armazenamento. | Sim | n/d | n/d |

<br>

## Relatório de erro original {#original-error-reporting}

Esta seção descreve o sistema original de relatório de erros, juntamente com os códigos de erro originais. No sistema original de relatório de erros, o AccessEnabler transmite erros para estas duas funções de retorno de chamada: `setAuthenticationStatus()` após uma chamada para `checkAuthentication()`; `tokenRequestFailed()`, após a falha de uma chamada para `checkAuthorization()` ou `getAuthorization()`.

O relatório de erros original e as APIs de status continuam a funcionar exatamente como antes. No entanto, a partir de agora, as APIs originais de relatórios de erros não serão atualizadas. Todos os novos relatórios de erros e atualizações sobre os erros antigos serão refletidos SOMENTE na nova [Sistema de Relatório de Erros Avançado](#advanced-error-reporting).


Para obter exemplos de uso do sistema original de relatório de erros, consulte o [Referência da API JavaScript](/help/authentication/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) e [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) funções, [Referência da API do iOS/tvOS](/help/authentication/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)e [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed), [Referência da API do Android](/help/authentication/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) e [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### Códigos de erro de chamada de retorno originais {#original-callback-error-codes}

| **Erros genéricos** |  |
|---|---|
| Erro interno | Ocorreu um erro de sistema ao tentar processar a solicitação. |
| Erro do Provedor não Selecionado | Ocorre quando o cliente é cancelado na caixa de diálogo de seleção do provedor. |
| Erro de Provedor Não Disponível | Ocorre quando nenhum provedor está disponível. |
|  |  |
| **Erros de autenticação** |  |
| Erro de Autenticação Genérica | Retornado quando o motivo não é conhecido ou não pode ser publicado. |
| Erro de Autenticação Interna | Ocorreu um erro de sistema ao tentar autenticar. |
| Erro de Usuário Não Autenticado | O usuário não está autenticado. |
|  |  |
| **Erros de autorização** |  |
| Erro de Autorização Genérica | Retornado quando o motivo não é conhecido ou não pode ser publicado. |
| Erro de Autorização Interna | Ocorreu um erro de sistema ao tentar autorizar. |
| Erro de Usuário não Autorizado | O cliente não está autorizado a visualizar o conteúdo solicitado. |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->