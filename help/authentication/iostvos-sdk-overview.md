---
title: Visão geral do SDK do iOS/tvOS
description: 'Visão geral do SDK do iOS/tvOS '
source-git-commit: 6b9508e56bdaa4876bd0974bf7877fb0c1810919
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Visão geral do SDK do iOS/tvOS {#iostvos-sdk-overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


</br>


## Introdução {#intro}

O iOS AccessEnabler é uma biblioteca Objetive-C iOS/tvOS que permite que aplicativos móveis usem a autenticação Adobe Primetime para os serviços de direito da TV em qualquer lugar. A implementação consiste no *AccessEnabler* interface que define a API de direito e a *EntitlementDelegate* e *[EntitlementStatus](#ios%20entitlement%20status)* protocolos que descrevem os retornos de chamada que a biblioteca aciona. A interface, juntamente com o protocolo, é referida com um nome comum: a biblioteca AccessEnabler.

## Requisitos do iOS e tvOS {#reqs}

Para os requisitos técnicos atuais relacionados à plataforma iOS e tvOS e à Autenticação do Primetime, consulte [Requisitos de plataforma/dispositivo/ferramenta](#ios)e consulte as notas de versão incluídas no download do SDK. Durante o restante desta página, você verá seções que notam alterações que se aplicam a versões específicas do SDK e superiores. Por exemplo, a seguinte é uma observação legítima em relação ao SDK 1.7.5:

## Noções básicas sobre workflows de clientes nativos {#flows}

Os workflows do cliente nativo normalmente são iguais ou muito semelhantes aos dos clientes de autenticação do Primetime baseados em navegador. No entanto, há algumas exceções, conforme descrito abaixo.

- [Fluxo de trabalho pós-inicialização](#post-init)
- [Fluxo de trabalho de autenticação inicial genérico](#generic)
- [Fluxo de trabalho de logout](#logout)


### Fluxo de trabalho pós-inicialização {#post-init}

Todos os workflows de direito suportados pelo AccessEnabler pressupõem que você já tenha chamado anteriormente [`setRequestor()`](#setReq) para estabelecer sua identidade. Você faz esta chamada para fornecer sua ID de Solicitante apenas uma vez, normalmente durante a fase de inicialização/configuração do aplicativo.


Com um cliente nativo do iOS, após a chamada inicial para [`setRequestor()`](#setReq), você tem a opção de saber como proceder:

- Você pode começar a fazer chamadas de direito imediatamente e permitir que elas sejam enfileiradas silenciosamente, se necessário.

- Você pode receber uma confirmação do sucesso/falha de [`setRequestor()`](#setReq) , mediante a aplicação [`setRequestorComplete()`](#setReqComplete) retorno de chamada.

- Você pode fazer as duas opções acima.

Escolha fazer com que o aplicativo aguarde a notificação do sucesso do [`setRequestor()`](#setReq) ou faça com que ele dependa do mecanismo de fila de chamadas do AccessEnabler. Como todas as solicitações de autorização e autenticação subsequentes precisam da ID do solicitante e das informações de configuração associadas, a variável [`setRequestor()`](#setReq) O método bloqueia efetivamente todas as chamadas da API de autenticação e autorização até que a inicialização seja concluída.

 

### Fluxo de trabalho de autenticação inicial genérico {#generic}

O objetivo deste fluxo de trabalho é fazer logon em um usuário com seu MVPD. Após um logon bem-sucedido, o servidor de back-end emite um token de autenticação para o usuário. Embora a autenticação normalmente seja feita como parte do processo de autorização, o seguinte descreve como a autenticação pode funcionar de forma isolada e não inclui nenhuma etapa de autorização.

Observe que, embora esse fluxo de trabalho seja diferente para clientes nativos do fluxo de trabalho de autenticação típico baseado em navegador, as etapas 1 a 5 são as mesmas para clientes nativos e clientes baseados em navegador.

1. Seu aplicativo inicia o fluxo de trabalho de autenticação com uma chamada para o `getAuthentication() `Método API, que verifica se há um token de autenticação em cache válido.
1. Se o usuário estiver autenticado no momento, o AccessEnabler chamará seu [`setAuthenticationStatus()`](#setAuthNStatus) função de retorno de chamada, passagem de um status de autenticação indicando sucesso e término do fluxo.
1. Se o usuário não estiver autenticado no momento, o AccessEnabler continuará o fluxo de autenticação determinando se a última tentativa de autenticação do usuário foi bem-sucedida com um determinado MVPD. Se uma ID MVPD estiver armazenada em cache E a variável `canAuthenticate` sinalizador é verdadeiro OU um MVPD foi selecionado usando [`setSelectedProvider()`](#setSelProv), o usuário não é solicitado com a caixa de diálogo de seleção MVPD. O fluxo de autenticação continua usando o valor em cache do MVPD (ou seja, o mesmo MVPD que foi usado durante a última autenticação bem-sucedida). Uma chamada de rede é feita ao servidor de backend e o usuário é redirecionado para a página de logon do MVPD (Etapa 6 abaixo).
1. Se nenhuma ID MVPD estiver armazenada em cache E nenhum MVPD tiver sido selecionado usando [`setSelectedProvider()`](#setSelProv) OU a `canAuthenticate` sinalizador é definido como falso, a variável [`displayProviderDialog()`](#dispProvDialog) o retorno de chamada é chamado. Este retorno de chamada instrui seu aplicativo a criar a interface do usuário que apresenta ao usuário uma lista de MVPDs para escolher. Uma matriz de objetos MVPD é fornecida, contendo as informações necessárias para você criar o seletor MVPD. Cada objeto MVPD descreve uma entidade MVPD e contém informações como a ID do MVPD (por exemplo, XFINITY, AT\&amp;T etc.) e o URL onde o logotipo MVPD pode ser encontrado.
1. Depois que um MVPD específico é selecionado, o aplicativo deve informar o AccessEnabler da escolha do usuário. Depois que o usuário selecionar o MVPD desejado, você informará o AccessEnabler da seleção do usuário por meio de uma chamada para o [`setSelectedProvider()`](#setSelProv) método .
1. O iOS AccessEnabler chama sua `navigateToUrl:` retorno de chamada ou `navigateToUrl:useSVC:` retorno de chamada para redirecionar o usuário para a página de logon do MVPD. Ao acionar qualquer um, o AccessEnabler faz uma solicitação para que o aplicativo crie um `UIWebView/WKWebView or SFSafariViewController` e para carregar o URL fornecido no `url` parâmetro. Esse é o URL do endpoint de autenticação no servidor de back-end. Para tvOS AccessEnabler, a variável [status()](#status_callback_implementation) o retorno de chamada é chamado com um `statusDictionary` e a pesquisa para a autenticação da segunda tela é iniciada imediatamente. O `statusDictionary` contém a variável `registration code` que precisa ser usado para a autenticação da segunda tela. 
1. No caso do iOS AccessEnabler, o usuário acessa a página de logon do MVPD para inserir suas credenciais por meio do aplicativo `UIWebView/WKWebView or SFSafariViewController `controladora. Observe que várias operações de redirecionamento ocorrem durante essa transferência e seu aplicativo deve monitorar os URLs que são carregados pelo controlador durante as várias operações de redirecionamento.
1. No caso do iOS AccessEnabler, quando a variável `UIWebView/WKWebView or SFSafariViewController` O controlador carrega um URL personalizado específico que o aplicativo deve fechar o controlador e chamar o do AccessEnabler `handleExternalURL:url `Método da API. Observe que esse URL personalizado específico é inválido e não se destina ao controlador realmente carregá-lo. Ele deve ser interpretado somente pelo seu aplicativo como um sinal de que o fluxo de autenticação foi concluído e de que é seguro fechar o `UIWebView/WKWebView or SFSafariViewController` controladora. Caso seu aplicativo seja necessário usar um `SFSafariViewController `controladora o URL personalizado específico é definido pela variável `application's custom scheme` (por exemplo: `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), caso contrário, esse URL personalizado específico será definido pela variável `ADOBEPASS_REDIRECT_URL` constante (ou seja, `adobepass://ios.app`).
1. Quando o aplicativo fechar o `UIWebView/WKWebView or SFSafariViewController` controlador e chama AccessEnabler `handleExternalURL:url `Método API, o AccessEnabler recupera o token de autenticação do servidor de back-end e informa ao aplicativo que o fluxo de autenticação foi concluído. O AccessEnabler chama a função [`setAuthenticationStatus()`](#setAuthNStatus) retorno de chamada com um código de status 1, indicando sucesso. Se houver um erro durante a execução dessas etapas, a variável [`setAuthenticationStatus()`](#setAuthNStatus) O retorno de chamada é acionado com um código de status de 0, indicando falha de autenticação, bem como um código de erro correspondente.


>[!WARNING]
>
> Durante as etapas em que o AccessEnabler rende controle ao seu aplicativo (ou seja, quando a caixa de diálogo de seleção do provedor é exibida ou quando UIWebView/WKWebView ou SFSafariViewController é exibida), o usuário tem a oportunidade de cancelar o fluxo de autenticação. Nessas situações, o aplicativo é responsável por informar o AccessEnabler sobre esse evento e chamar a função [`setSelectedProvider()`](#setSelProv) Método da API, passando null como parâmetro. Isso dá ao AccessEnabler a chance de limpar seu estado interno e redefinir o fluxo de autenticação. No tvOS, você pode usar o mesmo método para cancelar a pesquisa de autenticação.


### Fluxo de trabalho de logout {#logout}

Para clientes nativos, o logout é feito de forma semelhante ao processo de autenticação descrito acima.

1. Seu aplicativo inicia o fluxo de trabalho de logout com uma chamada para o `logout() `Método da API. O logout é o resultado de uma série de operações de redirecionamento HTTP porque o usuário precisa ser desconectado dos servidores de Autenticação Primetime e também dos servidores MVPD. Como esse fluxo não pode ser concluído com uma simples solicitação HTTP emitida pela biblioteca do AccessEnabler, um `UIWebView/WKWebView or SFSafariViewController` O controlador precisa ser instanciado para poder seguir as operações de redirecionamento HTTP.

1. É utilizado um padrão semelhante ao fluxo de autenticação. O iOS AccessEnabler aciona o `navigateToUrl:` retorno de chamada ou a variável `navigateToUrl:useSVC:` para criar um `UIWebView/WKWebView or SFSafariViewController` e para carregar o URL fornecido no `url` parâmetro. Esse é o URL do endpoint de logout no servidor de back-end. Para o tvOS AccessEnabler, nenhuma das variáveis `navigateToUrl:` retorno de chamada ou a variável `navigateToUrl:useSVC:` o retorno de chamada é chamado.

1. Conforme ele passa por vários redirecionamentos, seu aplicativo deve monitorar a atividade do `UIWebView/WKWebView or SFSafariViewController `e detectar o momento em que carrega um URL personalizado específico. Observe que esse URL personalizado específico é inválido e não se destina ao controlador realmente carregá-lo. Ele só deve ser interpretado pelo seu aplicativo como um sinal de que o fluxo de logout foi concluído e de que é seguro fechar o controlador. Quando o controlador carrega esse URL personalizado específico, seu aplicativo deve fechar o controlador e chamar o `handleExternalURL:url `Método da API. Caso seu aplicativo seja necessário usar um `SFSafariViewController `controladora o URL personalizado específico é definido pela variável `application's custom scheme` (por exemplo,`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), caso contrário, esse URL personalizado específico será definido pela variável ` ADOBEPASS_REDIRECT_URL  `constante (ou seja, `adobepass://ios.app`).

1. No final, o AccessEnabler chamará a função [`setAuthenticationStatus()`](#setAuthNStatus) retorno de chamada com um código de status igual a 0, indicando o sucesso do fluxo de logout.

O fluxo de logout é diferente do fluxo de autenticação, pois o usuário não precisa interagir com o `UIWebView/WKWebView or SFSafariViewController`  de qualquer maneira. Portanto, o Adobe recomenda que você torne o controle invisível (ou seja, oculto) durante o processo de logout.

## Tokens {#tokens}

- [Definições e uso](#definitions)
- [Diretrizes de armazenamento em cache](#caching)
- [Persistência](#persistence)
- [Formato](#format)
- [Vínculo do dispositivo](#device_binding)


### Definições e uso {#definitions}

A solução de direito de autenticação Primetime envolve a geração de partes específicas de dados (tokens) geradas pela autenticação do Primetime após a conclusão com êxito dos workflows de autenticação e autorização. Esses tokens são armazenados localmente no dispositivo iOS do cliente.

 

Os tokens têm uma duração limitada; após a expiração, os tokens precisam ser reemitidos por meio do reinício dos workflows de autenticação e/ou autorização.

 

Há três tipos de tokens emitidos durante os workflows de direito:

- **Token de autenticação:** O resultado final do fluxo de trabalho de autenticação do usuário será um GUID de autenticação que o AccessEnabler poderá usar para fazer consultas de autorização em nome do usuário. Esse GUID de autenticação terá um valor TTL (time-to-live) associado que pode ser diferente da própria sessão de autenticação do usuário. Um token de autenticação será gerado vinculando o GUID de autenticação ao dispositivo que inicia as solicitações de autenticação.
- **Token de autorização:** Concede acesso a um recurso protegido específico identificado por um resourceID exclusivo. Consiste em uma concessão de autorização emitida pela parte emissora junto com a resourceID original. Essas informações estão vinculadas ao dispositivo que inicia a solicitação.
- **Token de mídia de curta duração:** O AccessEnabler concede acesso ao aplicativo de hospedagem para um determinado recurso ao retornar um token de mídia de curta duração. Esse token é gerado com base no token de autorização adquirido anteriormente para esse recurso específico. Além disso, esse token não está vinculado ao dispositivo e a duração associada é significativamente menor (padrão: 5 minutos).

Após a autenticação e a autorização bem-sucedidas, a autenticação do Primetime emitirá a autenticação, a autorização e os tokens de mídia de curta duração. Esses tokens devem ser armazenados em cache no dispositivo do usuário e usados pela duração de suas extensões de vida associadas.

 

### Diretrizes de armazenamento em cache {#caching}

- Token de autenticação
- Token de autorização
- Token de mídia de duração curta


#### Token de autenticação

- **AccessEnabler 1.7:** Este SDK introduz um novo método de armazenamento de tokens, permitindo vários buckets do Programador-MVPD e, portanto, vários tokens de autenticação. Agora, o mesmo layout de armazenamento é usado tanto para o cenário &quot;Autenticação por Solicitante&quot; quanto para o fluxo de autenticação normal. A única diferença entre os dois é na maneira como a autenticação é executada: &quot;Autenticação por Solicitante&quot; contém um novo aprimoramento (Autenticação Passiva) que possibilita que o AccessEnabler execute autenticação de canal traseiro, com base na existência de um token de autenticação no armazenamento (para um Programador diferente). O usuário só precisa se autenticar uma vez e essa sessão será usada para obter tokens de autenticação em aplicativos adicionais. Esse fluxo de canal traseiro ocorre durante a [`setRequestor()`](#setReq) O é mais transparente para o Programador. **Há, no entanto, um requisito importante aqui: o programador DEVE chamar setRequestor() do encadeamento principal da interface do usuário.**
- **AccessEnabler 1.6 e posterior:** A maneira como os tokens de autenticação são armazenados em cache no dispositivo depende do &quot;**Autenticação por solicitante&quot;** sinalizador associado ao MVPD atual:

<!-- end list -->

1. Se o recurso &quot;Autenticação por solicitante&quot; estiver desativado, um único token de autenticação será armazenado localmente na área de transferência global; esse token será compartilhado entre todos os aplicativos integrados com o MVPD atual.
1. Se o recurso &quot;Autenticação por Solicitante&quot; estiver ativado, um token será explicitamente associado ao Programador que executou o fluxo de autenticação (o token não será armazenado na área de transferência global, mas em um arquivo privado visível somente para o aplicativo desse Programador). Mais especificamente, o Single Sign-On (SSO) entre diferentes aplicativos será desativado; o usuário precisará executar o fluxo de autenticação explicitamente ao alternar para um novo aplicativo (fornecendo o fato de que o Programador do segundo aplicativo está integrado ao MVPD atual e que não existe nenhum token de autenticação para esse Programador no cache local).

 

#### Token de autorização

A qualquer momento, apenas UM token de autorização POR RECURSO é armazenado em cache pelo AccessEnabler. Pode haver vários tokens de autorização em cache, mas eles estão associados a recursos diferentes. Sempre que um novo token de autorização é emitido e já existe um antigo para *o mesmo recurso*, o novo token substitui o valor em cache existente.

 

#### Token de mídia

O token de mídia de curta duração NÃO deve ser armazenado em cache. O token de mídia deve ser recuperado do servidor sempre que uma API de autorização for chamada, pois está restrito ao uso único.

 

### Persistência {#persistence}

Os tokens precisam ser persistentes em execuções consecutivas do mesmo aplicativo. Isso significa que, uma vez que os tokens de autenticação e autorização tenham sido adquiridos e o usuário feche o aplicativo, os mesmos tokens estarão disponíveis para o aplicativo quando o usuário reabrir o aplicativo. Além disso, é desejável que esses tokens sejam persistentes em vários aplicativos. Em outras palavras, depois que um usuário usa um aplicativo para fazer logon com um provedor de identidade específico (obtendo tokens de autenticação e autorização com êxito), os mesmos tokens podem ser usados por meio de um aplicativo diferente, e o usuário não é mais solicitado a fornecer credenciais ao fazer logon por meio do mesmo provedor de identidade. Esse tipo de fluxo de trabalho de autenticação/autorização simples é o que torna a solução de autenticação Primetime uma implementação TV-Em qualquer lugar verdadeira. 

 

## iOS

A biblioteca iOS AccessEnabler funciona com relação aos problemas de compartilhamento de dados entre aplicativos armazenando os dados do token em uma estrutura de dados &quot;semelhante à área de transferência&quot; chamada de *colar quadro*. Esse recurso compartilhado em nível de sistema fornece os principais ingredientes que permitem a implementação do caso de uso de tokens persistentes desejado:

- **Suporte para armazenamento estruturado** - O quadro de colagem não é apenas uma estrutura de memória simples, linear e semelhante a buffer. Ele fornece um mecanismo de armazenamento semelhante ao dicionário que permite a indexação de dados com base em valores de chave especificados pelo usuário.
- **Suporte para persistência de dados usando o sistema de arquivos subjacente** - O conteúdo da estrutura da área de colagem pode ser marcado como persistente, nesse caso, os dados são salvos na memória interna do dispositivo.

 

Depois que um token específico é colocado no cache de token, sua validade será verificada em momentos diferentes pela biblioteca AccessEnabler.  Um token válido é definido como:

- O TTL do token não expirou.
- O emissor do token está incluído na lista de provedores de identidade permitidos.

 

## tvOS

Como na tvOS a área de transferência não está disponível, a biblioteca tvOS AccessEnabler usa o NsUserDefaults como uma opção de armazenamento. Isso soluciona o problema de tokens de autenticação e autorização persistentes, mas as informações armazenadas não podem ser compartilhadas entre aplicativos diferentes.

 

**Alterações na área de transferência do iOS 10 -** Ao atualizar de uma versão anterior do iOS, a área de transferência será apagada. Isso significa que todos os aplicativos precisam ser autenticados novamente.

 

**Alterações na área de transferência do iOS 7 -** Devido a alterações no funcionamento dos painéis no iOS 7, haverá um SSO cruzado limitado entre aplicativos em execução no iOS 7. Aplicações com as mesmas características `<Bundle Seed ID>`(também conhecido como `<Team ID>`) compartilhará tokens, o que significa que os aplicativos A1 e A2 do mesmo Programador X compartilharão tokens, enquanto o aplicativo A1 (Programador X) e o aplicativo A3 (Programador Y) não compartilharão tokens. 

- A ID de montagem do pacote/ID de equipe é a mesma entre dois aplicativos se eles forem gerados pelo mesmo perfil de provisionamento. Encontre mais informações neste link:
   [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html ](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- Essa limitação &quot;Cross SSO&quot; estará presente no iOS 7, independentemente do SDK de autenticação do Primetime usado. 

Leia esta nota técnica para obter mais informações sobre como configurar o SSO no iOS 7 e superior (a nota técnica se aplica ao Access Enabler v1.8 e superior): <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>

 

### Armazenamento de tokens (AccessEnabler 1.7)

A partir do AccessEnabler 1.7, o armazenamento de token pode suportar várias combinações Programmer-MVPD, dependendo de uma estrutura de mapa aninhada de vários níveis que pode conter vários tokens de autenticação. Esse novo armazenamento não afeta a API pública do AccessEnabler de nenhuma maneira e não requer alterações do lado do Programador. Este é um exemplo que ilustra esta nova funcionalidade:

1. Abra o App1 (desenvolvido pelo Programador1).
1. Autentique com MVPD1 (que é integrado com Programador1).
1. Suspender/fechar o aplicativo atual e abrir o App2 (desenvolvido pelo Programador2).
1. Vamos supor que o Programmer2 não está integrado ao MVPD2; portanto, o usuário NÃO será autenticado no App2.
1. Autentique com MVPD2 (que é integrado com Programador2) no App2.
1. Volte para App1; o usuário ainda será autenticado com Programador1.

Em versões anteriores do AccessEnabler, a Etapa 6 renderizaria o usuário como não autenticado, pois o armazenamento de token era compatível com apenas um token de autenticação.

 

Fazer logoff de uma sessão do Programador / MVPD limpará todo o armazenamento subjacente, incluindo todos os outros tokens de autenticação do Programador / MVPD no dispositivo. Por outro lado, cancelar o fluxo de autenticação (chamada de [`setSelectedProvider(null)`](#setSelProv)) NÃO limpará o armazenamento subjacente, mas afetará apenas a tentativa de autenticação atual do Programador / MVPD (apagando o MVPD do programador atual).

 

### Importador de token (AccessEnabler 1.7)

Outro recurso relacionado ao armazenamento incluído no AccessEnabler 1.7 possibilita importar tokens de autenticação de áreas de armazenamento mais antigas. Este &quot;Importador de Token&quot; ajuda a alcançar a compatibilidade entre versões consecutivas do AccessEnabler, mantendo o estado SSO mesmo quando a versão de armazenamento é atualizada. O importador é executado durante a [`setRequestor()`](#setReq) e é executado nos dois cenários a seguir (supondo que nenhum token de autenticação válido para o Programador atual esteja presente no armazenamento atual):

- A primeira instalação de um aplicativo 1.7 desenvolvido por um programador específico
- Atualizar caminho para um AccessEnabler futuro que use um novo armazenamento

A operação de importação é transparente para o Programador e não requer nenhuma alteração de código no aplicativo cliente.

 

### Token Sanitizer (AccessEnabler 1.7.5)

A partir do AccessEnabler 1.7.5, esse serviço é executado em [`setRequestor()`](#setReq)`. `Ela foi desenvolvida como resultado da troca do iOS 7 do endereço MAC WiFi para o IDFA para rastreamento. O sanitizer garante que o armazenamento atual contenha apenas tokens de autenticação válidos (válidos em termos da ID do dispositivo, anteriormente calculados usando o endereço do MAC, antes do iOS7). O Token Sanitizer remove todos os tokens inválidos. 

 

O serviço Token Sanitizer é mais útil quando um aplicativo AccessEnabler 1.7.5 é usado no iOS 6 e o usuário atualiza para o iOS 7. Quando isso acontece, todos os tokens de autenticação obtidos no iOS 6 agora são inválidos (devido à alteração do algoritmo de ID de dispositivo de uso do endereço MAC para o IDFA). O depurador limpará todos os tokens inválidos e o usuário não será autenticado. 

 

Sem o Token Sanitizer removendo tokens inválidos, o AccessEnabler não obteria autorizações devido à presença de tokens de autenticação inválidos. Isso seria complicado para o usuário final depurar, já que as mensagens de erro de autorização podem ser criptografadas e não muito úteis para determinar o que causou o problema. 

 

### Formato {#format}

- [Token de AuthN](#authn_token)
- [Token de AuthZ](#authz_token)
- [Token de mídia curta](#short_token)
- [Vínculo do dispositivo](#device_binding)


Observe que o formato dos tokens AuthN e AuthZ está incluído aqui apenas para informações de fundo. A estrutura desses tokens pode ser alterada pela autenticação do Primetime a qualquer momento. Os programadores não precisam saber a estrutura exata dos tokens AuthN e AuthZ para implementar seus aplicativos, pois os tokens AuthN e AuthZ não são expostos no dispositivo local. O token de mídia curta *é* exposto ao aplicativo do Programador.

 

#### Token de autenticação {#authn_token}

A listagem abaixo apresenta o formato do token de autenticação:

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthenticationToken>
      <simpleTokenAuthenticationGuid>71C69B91-F327-F185-F29E-2CE20DC560F5</simpleTokenAuthenticationGuid>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenDomainName>adobe.com</simpleTokenDomainName>
      <simpleTokenExpires>2011/03/19 02:29:34 GMT +0200</simpleTokenExpires>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>   
  </simpleAuthenticationToken>
```
 

#### Token de autorização {#authz_token}

A lista seguinte apresenta o formato do token de autorização:

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthorizationToken>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenResourceID>TEST_RESOURCE</simpleTokenResourceID>
      <simpleTokenTTL>2011/03/17 14:40:08 GMT +0200</simpleTokenTTL>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>
  </simpleAuthorizationToken>
```
 

#### Token de mídia curta {#short_token}

A listagem abaixo apresenta o formato do token de mídia curto. Esse token é exposto ao aplicativo do Programador. Ele é passado para o aplicativo do Programador no final de um processo de direito bem-sucedido:

```
  <signatureInfo>signature<signatureInfo>
  <shortAuthorizationToken>
    <sessionGUID>session_guid</sessionGUID>
    <requestorID>requestor_id</requestorID>
    <resourceID>resource_id</resourceID>
    <ttl>ttl_in_ms</ttl>
    <issueTime>issue_time</issueTime>
    <mvpdId>mvpd_id</mvpdId>
    <proxyMvpdId>proxy_mvpd_id</proxyMvpdId>
  </shortAuthorizationToken>
```
 

### Vínculo do dispositivo {#device_binding}

Nas listagens XML acima, observe a tag intitulada `simpleTokenFingerprint`. A finalidade dessa tag é manter informações de individualização da ID do dispositivo nativa. A biblioteca AccessEnabler pode obter essas informações de individualização e disponibilizá-las para os serviços de autenticação do Primetime durante as chamadas de direito. O serviço usará essas informações e as incorporará aos tokens reais, vinculando efetivamente os tokens a um dispositivo específico. O objetivo final disso é tornar os tokens não transferíveis entre os dispositivos.

 

Como é óbvio que se trata de um recurso relacionado com a segurança, estas informações são inerentemente &quot;sensíveis&quot; do ponto de vista da segurança. Como resultado, essas informações precisam ser protegidas contra adulterações e escutas. O problema de escuta é resolvido enviando as solicitações de autenticação/autorização pelo protocolo HTTPS. A proteção contra adulterações é feita assinando digitalmente as informações de identificação do dispositivo. A biblioteca AccessEnabler calcula uma ID de dispositivo das informações fornecidas pelo dispositivo, em seguida, envia a ID do dispositivo &quot;em claro&quot; para os servidores de autenticação do Primetime como um parâmetro de solicitação. Os servidores de autenticação do Primetime assinam digitalmente a ID do dispositivo com a chave privada Adobe e a adicionam ao token de autenticação retornado ao AccessEnabler. Assim, a ID do dispositivo é vinculada ao token de autenticação. Durante o fluxo de autorização, o AccessEnabler envia novamente a ID do dispositivo na limpeza, juntamente com o token de autenticação. A falha do processo de validação resultará automaticamente em falha dos workflows de autenticação/autorização. Os servidores de autenticação do Primetime aplicam a chave privada à ID do dispositivo e a comparam com o valor no token de autenticação. Se não corresponderem, esse fluxo de direito falhará.

 

**Observação sobre Vínculo de dispositivo no AccessEnabler 1.7.5:** A partir do AccessEnabler 1.7.5, há uma alteração em como a ID do dispositivo é calculada para fornecer informações de individualização para um dispositivo iOS. Essa alteração reflete uma alteração no iOS 7: No iOS 7, a Apple não fornece mais o endereço do MAC WiFi como opção de rastreamento, em favor do Identificador para anunciantes (IDFA). Como as informações de individualização de um aplicativo em execução no iOS 7 são baseadas no IDFA e são incorporadas nos tokens do fluxo de direito, isso significa que há vários efeitos diferentes possíveis na experiência do usuário que resultam dessa alteração. Os diferentes efeitos possíveis são baseados em qual versão do iOS o usuário está atualizando, combinada com qual versão do AccessEnabler o Programador está atualizando. Para obter detalhes sobre essa alteração, consulte as Notas de versão incluídas no SDK do AccessEnabler 1.7.5.


## Informações relacionadas {#related}

<!--
- [iOS/tvOS Integration Cookbook](#)
- [iOS/tvOS API Reference](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Primetime
  authentication native SDK (Tech Note)](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [SSO on iOS when using the Primetime authentication Access
  Enabler](#)
-->
