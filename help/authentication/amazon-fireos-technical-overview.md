---
title: Visão geral técnica do Amazon FireOS
description: Visão geral técnica do Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 0%

---


# Visão geral técnica do Amazon FireOS {#amazon-fireos-technical-overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

## Introdução {#intro}

O Amazon FireOS AccessEnabler é representado por dois componentes: Uma biblioteca stub AccessEnabler usada pelo aplicativo e uma biblioteca do Android Java no nível do sistema que permite que aplicativos móveis usem a autenticação Adobe Primetime para os serviços de direito da TV em qualquer lugar. Uma implementação do Android para o Amazon FireOS consiste na interface AccessEnabler que define a API de direito e um protocolo EntitlementDelegate que descreve os retornos de chamada que a biblioteca aciona. A biblioteca do Android AccessEnabler de nível de sistema permite o acesso a serviços da Amazon para ativar o Single Sing On no nível da plataforma.

## Noções básicas sobre workflows de clientes nativos {#native_client_workflows}

Os workflows do cliente nativo normalmente são iguais ou muito semelhantes aos dos clientes de autenticação do Primetime baseados em navegador. No entanto, há algumas exceções, conforme descrito abaixo.


### Fluxo de trabalho pós-inicialização {#post-init}

Todos os workflows de direito suportados pelo AccessEnabler pressupõem que você já tenha chamado anteriormente [`setRequestor()`](#setRequestor) para estabelecer sua identidade. Você faz esta chamada para fornecer sua ID de Solicitante apenas uma vez, normalmente durante a fase de inicialização/configuração do aplicativo.

Com os clientes nativos (por exemplo, AmazonFireOS), após a chamada inicial para [`setRequestor()`](#setRequestor), você tem a opção de saber como proceder:

- Você pode começar a fazer chamadas de direito imediatamente e permitir que elas sejam enfileiradas silenciosamente, se necessário.
- Ou você pode receber uma confirmação do sucesso/falha de [`setRequestor()`](#setRequestor) ao implementar o retorno de chamada setRequestorComplete().
- Ou faça ambos.

Cabe a você saber se deve aguardar a notificação do sucesso de [`setRequestor()`](#setRequestor) ou para confiar no mecanismo de fila de chamadas do AccessEnabler. Como todas as solicitações de autorização e autenticação subsequentes precisam da ID do solicitante e das informações de configuração associadas, a variável [`setRequestor()`](#setRequestor) O método bloqueia efetivamente todas as chamadas da API de autenticação e autorização até que a inicialização seja concluída.

### Fluxo de trabalho de autenticação inicial genérico {#generic}

O objetivo deste fluxo de trabalho é fazer logon em um usuário com seu MVPD.  Após um logon bem-sucedido, o servidor de back-end emite um token de autenticação para o usuário. Embora a autenticação normalmente seja feita como parte do processo de autorização, o seguinte descreve como a autenticação pode funcionar de forma isolada e não inclui nenhuma etapa de autorização.

Observe que, embora o fluxo de trabalho nativo do cliente a seguir seja diferente do fluxo de trabalho de autenticação típico com navegador, as etapas 1 a 5 são as mesmas para clientes nativos e clientes baseados em navegador:

1. Sua página ou reprodutor inicia o fluxo de trabalho de autenticação com uma chamada para [getAuthentication()](#getAuthN), que verifica se há um token de autenticação em cache válido. Este método tem um `redirectURL` parâmetro; se você não fornecer um valor para `redirectURL`, após uma autenticação bem-sucedida, o usuário é retornado ao URL do qual a autenticação foi inicializada.
1. O AccessEnabler determina o status de autenticação atual. Se o usuário estiver autenticado no momento, o AccessEnabler chamará seu `setAuthenticationStatus()` função de retorno de chamada, transmitindo um status de autenticação indicando sucesso (Etapa 7 abaixo).
1. Se o usuário não estiver autenticado, o AccessEnabler continuará o fluxo de autenticação determinando se a última tentativa de autenticação do usuário foi bem-sucedida com um determinado MVPD. Se uma ID MVPD estiver armazenada em cache E a variável `canAuthenticate` sinalizador é verdadeiro OU um MVPD foi selecionado usando [`setSelectedProvider()`](#setSelectedProvider), o usuário não é solicitado com a caixa de diálogo de seleção MVPD. O fluxo de autenticação continua usando o valor em cache do MVPD (ou seja, o mesmo MVPD que foi usado durante a última autenticação bem-sucedida). Uma chamada de rede é feita ao servidor de backend e o usuário é redirecionado para a página de logon do MVPD (Etapa 6 abaixo).
1. Se nenhuma ID MVPD estiver armazenada em cache E nenhum MVPD tiver sido selecionado usando [`setSelectedProvider()`](#setSelectedProvider) OU a `canAuthenticate` sinalizador é definido como falso, a variável [`displayProviderDialog()`](#displayProviderDialog) o retorno de chamada é chamado. Esse retorno de chamada direciona sua página ou reprodutor para criar a interface do usuário que apresenta ao usuário uma lista de MVPDs para escolher. Uma matriz de objetos MVPD é fornecida, contendo as informações necessárias para você criar o seletor MVPD. Cada objeto MVPD descreve uma entidade MVPD e contém informações como a ID do MVPD (por exemplo, XFINITY, AT\&amp;T etc.) e o URL onde o logotipo MVPD pode ser encontrado.
1. Depois que um MVPD específico é selecionado, sua página ou player deve informar ao AccessEnabler a escolha do usuário. Para clientes que não são Flash, depois que o usuário seleciona o MVPD desejado, você informa o AccessEnabler da seleção do usuário por meio de uma chamada para o [`setSelectedProvider()`](#setSelectedProvider) método . Os clientes do Flash, em vez disso, despacham um `MVPDEvent` do tipo &quot;`mvpdSelection`&quot;, transmitindo o provedor selecionado.
1. Para aplicativos Amazon, a variável [`navigateToUrl()`](#navigagteToUrl) o retorno de chamada será ignorado. A biblioteca de Ativador de Acesso facilita o acesso a um controle comum do WebView para autenticar usuários.
1. Por meio do `WebView`, o usuário chega à página de logon do MVPD e insere suas credenciais. Observe que várias operações de redirecionamento ocorrem durante essa transferência. 
1. Quando o WebView finalizar a autenticação, ele fechará e informará ao AccessEnabler que o usuário fez logon com êxito, o AccessEnabler recuperará o token de autenticação real do servidor de back-end. O AccessEnabler chama a função [`setAuthenticationStatus()`](#setAuthNStatus) retorno de chamada com um código de status 1, indicando sucesso. Se houver um erro durante a execução dessas etapas, a variável [`setAuthenticationStatus()`](#setAuthNStatus) O retorno de chamada é acionado com um código de status de 0, juntamente com um código de erro correspondente, indicando que o usuário não está autenticado.

### Fluxo de trabalho de logout {#logout}

Para clientes nativos, os logouts são manipulados de forma semelhante ao processo de autenticação descrito acima. Seguindo este padrão, o AccessEnabler criará um `WebView` controle e carregará o controle com a URL do endpoint de logout no servidor de back-end. Quando o processo de logout for concluído, os tokens serão apagados.

Observe que o fluxo de logout é diferente do fluxo de autenticação, já que o usuário não é obrigado a interagir com o `WebView` de qualquer maneira. Quando o logout for concluído, o AccessEnabler chamará a função `setAuthenticationStatus()` retorno de chamada com um código de status igual a 0, indicando que o usuário não está autenticado.

## Tokens {#tokens}

### Definições e uso {#definitions}

A solução de direito de autenticação Primetime envolve a geração de partes específicas de dados (tokens) geradas pela autenticação do Primetime após a conclusão com êxito dos workflows de autenticação e autorização. Esses tokens são armazenados localmente no dispositivo Amazon FireOS do cliente.

Os tokens têm uma duração limitada; após a expiração, os tokens precisam ser reemitidos por meio do reinício dos fluxos de trabalho de autenticação e/ou autorização.

Há três tipos de tokens emitidos durante os workflows de direito:

- **Token de autenticação** - O resultado final do fluxo de trabalho de autenticação do usuário será um GUID de autenticação que o AccessEnabler poderá usar para fazer consultas de autorização em nome do usuário. Esse GUID de autenticação terá um valor TTL (time-to-live) associado que pode ser diferente da própria sessão de autenticação do usuário. A autenticação do Primetime gera um token de autenticação ao vincular o GUID de autenticação ao dispositivo que inicia as solicitações de autenticação.
- **Token de autorização** - Concede acesso a um recurso protegido específico identificado por um `resourceID`. Consiste numa subvenção de autorização emitida pela entidade emissora juntamente com o original `resourceID`. Essas informações estão vinculadas ao dispositivo que inicia a solicitação.
- **Token de mídia de duração curta** - O AccessEnabler concede acesso ao aplicativo de hospedagem para um determinado recurso ao retornar um token de mídia de curta duração. Esse token é gerado com base no token de autorização adquirido anteriormente para esse recurso específico. Além disso, esse token não está vinculado ao dispositivo e a duração associada é significativamente menor (padrão: 5 minutos).

Após a autenticação e a autorização bem-sucedidas, a autenticação do Primetime emitirá a autenticação, a autorização e os tokens de mídia de curta duração. Esses tokens devem ser armazenados em cache no dispositivo do usuário e usados pela duração de suas extensões de vida associadas.

### Diretrizes de armazenamento em cache {#caching}


#### Token de autenticação

- **O AccessEnabler 1.10.1 para FireOS **é baseado no AccessEnabler para Android 1.9.1 - Esse SDK introduz um novo método de armazenamento de token, permitindo vários buckets do Programador-MVPD e, portanto, vários tokens de autenticação. 

#### Token de autorização

A qualquer momento, apenas UM token de autorização por recurso é armazenado em cache pelo AccessEnabler. Pode haver vários tokens de autorização em cache, mas eles estão associados a recursos diferentes. Sempre que um novo token de autorização for emitido e um antigo já existir para o mesmo recurso, o novo token substituirá o valor em cache existente.

#### Token de mídia 

O token de mídia de curta duração NÃO deve ser armazenado em cache. O token de mídia deve ser recuperado do servidor sempre que uma API de autorização for chamada, pois está restrito ao uso único.

### Persistência {#persistence}

Os tokens precisam ser persistentes em execuções consecutivas do mesmo aplicativo. Isso significa que, uma vez que os tokens de autenticação e autorização tenham sido adquiridos e o usuário feche o aplicativo, os mesmos tokens estarão disponíveis para o aplicativo quando o usuário reabrir o aplicativo. Além disso, é desejável que esses tokens sejam persistentes em vários aplicativos. Em outras palavras, depois que um usuário usa um aplicativo para fazer logon com um provedor de identidade específico (obtendo tokens de autenticação e autorização com êxito), os mesmos tokens podem ser usados por meio de um aplicativo diferente, e o usuário não é mais solicitado a fornecer credenciais ao fazer logon por meio do mesmo provedor de identidade.

Esse tipo de fluxo de trabalho de autenticação/autorização simples é o que torna a solução de autenticação Primetime uma implementação TV-Em qualquer lugar verdadeira. Do ponto de vista de engenharia puro, a biblioteca Android AccessEnabler resolve os problemas do compartilhamento de dados entre aplicativos armazenando os dados do token em um arquivo de banco de dados localizado no armazenamento externo. Esses recursos compartilhados em nível de sistema fornecem os principais ingredientes que permitem a implementação do caso de uso de tokens persistentes desejado:

- Suporte para armazenamento estruturado - o armazenamento de token de autenticação do Primetime não é apenas uma estrutura de memória linear simples, semelhante a buffer. Ele fornece um mecanismo de armazenamento semelhante ao dicionário que permite a indexação de dados com base em valores de chave especificados pelo usuário.
- Suporte para persistência de dados usando o sistema de arquivos subjacente - O conteúdo do arquivo de banco de dados é persistente por padrão e os dados são salvos na memória externa do dispositivo.

Depois que um token específico é colocado no cache de token, sua validade será verificada em momentos diferentes pela biblioteca AccessEnabler.  Um token válido é definido como:

- O TTL do token não expirou
- O emissor do token está incluído na lista de provedores de identidade permitidos

O armazenamento de token pode suportar várias combinações Programmer-MVPD, dependendo de uma estrutura de mapa aninhada de vários níveis que pode conter vários tokens de autenticação. Esse novo armazenamento não afeta a API pública do AccessEnabler de nenhuma maneira e não requer alterações do lado do Programador. Este é um exemplo que ilustra esta funcionalidade mais recente:

1. Abra o App1 (desenvolvido pelo Programador1).
1. Autentique com MVPD1 (que é integrado com Programador1).
1. Suspender/fechar o aplicativo atual e abrir o App2 (desenvolvido pelo Programador2).
1. Vamos supor que o Programmer2 não está integrado ao MVPD2; portanto, o usuário NÃO será autenticado no App2.
1. Autentique com MVPD2 (que é integrado com Programador2) no App2.
1. Volte para App1; o usuário ainda será autenticado com Programador1.

### Formato {#format}

#### Token de autenticação {#authn_token}

A listagem abaixo apresenta o formato do token de autenticação:

```JSON
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

```JSON
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


#### Token de mídia curta {#short_media_token}

A listagem abaixo apresenta o formato do token de mídia curto.  Esse token é exposto ao aplicativo do Programador.  Ele é passado para o aplicativo do Programador no final de um processo de direito bem-sucedido:

```JSON
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
 

#### Vínculo do dispositivo {#device_binding}

Nas listagens XML acima, observe a tag intitulada `simpleTokenFingerprint`. A finalidade dessa tag é manter informações de individualização da ID do dispositivo nativa. A biblioteca AccessEnabler pode obter essas informações de individualização e disponibilizá-las para os serviços de autenticação do Primetime durante as chamadas de direito. O serviço usará essas informações e as incorporará aos tokens reais, vinculando efetivamente os tokens a um dispositivo específico. O objetivo final disso é tornar os tokens não transferíveis entre os dispositivos.

Nas listagens XML acima, observe a tag intitulada simpleTokenFingerprint. A finalidade dessa tag é manter informações de individualização da ID do dispositivo nativa. A biblioteca AccessEnabler pode obter essas informações de individualização e disponibilizá-las para os serviços de autenticação do Primetime durante as chamadas de direito. O serviço usará essas informações e as incorporará aos tokens reais, vinculando efetivamente os tokens a um dispositivo específico. O objetivo final disso é tornar os tokens não transferíveis entre os dispositivos.

Como é óbvio que se trata de um recurso relacionado com a segurança, estas informações são inerentemente &quot;sensíveis&quot; do ponto de vista da segurança. Como resultado, essas informações precisam ser protegidas contra adulterações e escutas. O problema de escuta é resolvido enviando as solicitações de autenticação/autorização pelo protocolo HTTPS. A proteção contra adulterações é feita assinando digitalmente as informações de identificação do dispositivo. A biblioteca AccessEnabler calcula uma ID de dispositivo das informações fornecidas pelo dispositivo, em seguida, envia a ID do dispositivo &quot;em claro&quot; para os servidores de autenticação do Primetime como um parâmetro de solicitação.  Os servidores de autenticação do Primetime assinam digitalmente a ID do dispositivo com a chave privada Adobe e a adicionam ao token de autenticação retornado ao AccessEnabler. Assim, a ID do dispositivo é vinculada ao token de autenticação.  Durante o fluxo de autorização, o AccessEnabler envia novamente a ID do dispositivo na limpeza, juntamente com o token de autenticação.  A falha do processo de validação resultará automaticamente em falha dos workflows de autenticação/autorização.  Os servidores de autenticação do Primetime aplicam a chave privada à ID do dispositivo e a comparam com o valor no token de autenticação.  Se não corresponderem, esse fluxo de direito falhará.
