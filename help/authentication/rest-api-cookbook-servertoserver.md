---
title: Cookbook da API REST (servidor para servidor)
description: Servidor do guia da API rest para o servidor.
exl-id: 36ad4a64-dde8-4a5f-b0fe-64b6c0ddcbee
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 0%

---

# Cookbook da API REST (servidor para servidor) {#rest-api-cookbook-server-to-server}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.


## Visão geral {#overview}

O objetivo deste documento de guia é detalhar as práticas recomendadas para implementar a Autenticação do Adobe Primetime usando as arquiteturas de servidor para servidor.  Ele fornece requisitos básicos, implementação de fluxo passo a passo e considerações gerais para ambientes de produção e operação.

 

## Componentes {#components}

Em uma solução de servidor para servidor em funcionamento, os seguintes componentes estão envolvidos:

 
| Tipo Componente | | Descrição | | — | — | — | | Dispositivo de transmissão | Aplicativo de transmissão | O aplicativo Programador que reside no dispositivo de transmissão do usuário e reproduz o vídeo autenticado. | | | \[Opcional\] Módulo AuthN | se o dispositivo de transmissão tiver um agente do usuário (ou seja, navegador da Web), o módulo AuthN será responsável pela autenticação do usuário no IdP do MVPD. | | \[Opcional\] Dispositivo AuthN | Aplicativo AuthN | se o dispositivo de transmissão não tiver um agente do usuário (ou seja, navegador da Web), o aplicativo AuthN será um aplicativo Web de programador acessado de um dispositivo separado do usuário usando um navegador da Web. | | Infraestrutura do programador | Serviço de programador | Um serviço que vincula o dispositivo de transmissão ao serviço da Adobe Pass para obter decisões de autenticação e autorização. | | Infraestrutura Adobe Serviço Adobe Pass | | Um serviço que se integra ao MVPD IdP e ao Serviço AuthZ e fornece decisões de autenticação e autorização. | | Infraestrutura MVPD | IdP MVPD | Um terminal MVPD que fornece um serviço de autenticação baseado em credenciais para validar a identidade do usuário. | | | Serviço AuthZ do MVPD | Um terminal MVPD que fornece decisões de autorização com base nas assinaturas do usuário, controles dos pais etc. |


Os termos adicionais usados no fluxo são definidos no
[Glossário](/help/authentication/glossary.md).

## Fluxos {#flows}

### Registro dinâmico de cliente (DCR)


O Adobe Pass usa DCR para proteger as comunicações do cliente entre um aplicativo ou servidor do programador e os serviços da Adobe Pass. O fluxo do DCR é separado, dependente e de pré-requisito, e pode ser encontrado em [Registro de cliente dinâmico](/help/authentication/dynamic-client-registration.md).


### Autenticação (authN)

O fluxo de autenticação é usado para permitir que um usuário se identifique no MVPD para determinar se o usuário tem uma conta válida. 

1. O usuário inicia o aplicativo Dispositivo de streaming e tenta fazer logon ou visualizar conteúdo protegido.
2. O aplicativo Dispositivo de transmissão faz uma solicitação ao Serviço do programador para determinar se o dispositivo já está autenticado.
3. O Serviço do programador registra o aplicativo usando DCR.
4. O Serviço de programador verifica o status de autenticação do dispositivo de transmissão chamando o Serviço do Adobe Pass **checkauthn** API.
5. No caso de a **checkauthn** A chamada de retorna o status de que o Dispositivo do usuário é autenticado e, em seguida, o aplicativo pode prosseguir para o fluxo de autorização.
6. No caso de a **checkauthn** A chamada de retorna o status de que o dispositivo do usuário NÃO está autenticado, portanto, o aplicativo deve aguardar uma solicitação do usuário fazer logon.
7. Quando o usuário solicita o logon diretamente (por exemplo, seleciona o botão de logon) ou indiretamente (por exemplo, seleciona o conteúdo protegido quando ainda não está autenticado), o aplicativo Dispositivo de streaming faz uma solicitação ao Serviço do programador para iniciar a autenticação do usuário. O Serviço de programador solicita e recebe um código de registro exclusivo (regcode) ao chamar o Serviço do Adobe Pass **regcode** API.
8. O Serviço de programador também recupera a lista de MVPDs e atributos atuais chamando o Serviço do Adobe Pass **config** API. Observação: essa API também pode ser chamada anteriormente no fluxo e armazenada em cache.
9. O Serviço do programador retorna o regcode para o aplicativo Dispositivo de streaming e para a lista MVPD processada solicitada na etapa \#7. Nota: O formato de lista MVPD processado é especificado pelo Programador e pode ser filtrado para permitir ou bloquear explicitamente MVPDs específicos (isto é, listas de permissão ou de bloqueio).
10. Se for diferente do Dispositivo de autenticação (ou seja, &quot;segunda tela&quot;), por escolha ou necessidade (ou seja, o Dispositivo de transmissão não é compatível com um Agente do usuário), o Dispositivo de transmissão deverá exibir o regcode e um URI para que o usuário acesse o Aplicativo de autenticação. O usuário digita o URI no Agente do Usuário no Dispositivo AuthN para iniciar o Aplicativo AuthN e digita o regcode nesse aplicativo. Se o Dispositivo de transmissão for o mesmo que o Dispositivo AuthN, o regcode poderá ser transmitido programaticamente para o Módulo AuthN.
11. O Módulo AuthN inicia a autenticação do usuário com o MVPD exibindo um Seletor de MVPD. Depois que o usuário seleciona o MVPD, o Módulo de autenticação chama **autenticar** com o regcode, que redireciona o Agente do usuário para o IdP do MVPD. Quando o usuário é autenticado com êxito com o MVPD, o Agente do Usuário é redirecionado de volta por meio do Serviço do Adobe Pass, onde a autenticação bem-sucedida é registrada com o regcode e, em seguida, redirecionada de volta para o Módulo de Autenticação.
12. Se o dispositivo de transmissão for diferente do dispositivo de autenticação, o dispositivo de autenticação deverá exibir uma mensagem de autenticação bem-sucedida para o usuário e as etapas para continuar (por exemplo, &quot;Success\! Agora você pode voltar ao console de jogos para continuar ([...\]&quot;). Se o Dispositivo de transmissão for o mesmo que o Dispositivo de autenticação, o Dispositivo de transmissão pode detectar programaticamente a conclusão da autenticação.

 

O diagrama a seguir ilustra o fluxo de autenticação:

![](assets/authn-flow.png)

### Autorização (authZ)

O fluxo de autorização é usado para determinar se um usuário tem direito a acessar o conteúdo solicitado.

1. Toda vez que o usuário tenta visualizar o conteúdo protegido no aplicativo Dispositivo de transmissão, o aplicativo Dispositivo de transmissão chama o Serviço do programador identificando o conteúdo e solicitando a permissão e as informações necessárias para iniciar o fluxo.
1. O serviço do programador chama o Adobe Pass **authorize** API que transmite a ID do recurso juntamente com outros parâmetros necessários. O Serviço da Adobe chama o Serviço MVPD AuthZ com a ID de recurso e recebe uma decisão de autorização que, em seguida, é passada de volta para o Serviço do programador. Essa decisão de autorização será armazenada em cache pelo Serviço do Adobe Pass por um período configurável. Nos próximos **authorize** Chamadas do Serviço de programador para o Serviço do Adobe Pass, o valor em cache será retornado enquanto for válido.
1. Se a autorização for concedida, o Serviço de Programação deve chamar a Adobe Pass **/tokens/media** API, que retornará um token de mídia assinado. O Serviço de programador deve validar o token de mídia usando a biblioteca Media Token Verifier (JAR). Se for válido, o Serviço do programador deverá retornar a permissão e a permissão necessária para iniciar o fluxo (por exemplo, o URL do fluxo) solicitado na etapa \#1.
1. Se a autorização for negada, a variável **authorize** A chamada retornará um código de erro e uma descrição ao Serviço de programador. O Serviço do programador deve retornar o código de erro e a descrição (ou uma mensagem modificada pelo programador) para a solicitação na etapa \#1.

O diagrama a seguir ilustra o fluxo de autorização:

![](assets/authz-flow.png)

### Sair

O fluxo de logout permite que um usuário remova a identidade associada atualmente ao aplicativo.

1. Quando o usuário solicita o logout (ou seja, remove do dispositivo a conta MVPD atual associada ao aplicativo), o aplicativo Dispositivo de transmissão chama o Serviço do programador, informando para fazer logout do dispositivo.
1. O Serviço de programador deve chamar o Adobe Pass **logout** API.

O diagrama a seguir ilustra o fluxo de logout:

![](assets/logout-flow.png)

### \[Opcional\] Pré-autorização (também conhecido como Pré-voo)

A pré-autorização pode ser usada para determinar rapidamente, a partir de um conjunto de recursos, aqueles que um usuário pode ter acesso.  O resultado desta chamada geralmente é usado para personalizar a interface do usuário de um usuário individual.

1. Depois que o usuário é autenticado, o dispositivo de streaming pode chamar o serviço de programador para solicitar o conteúdo para o qual o usuário tem direito a streaming.

1. O Serviço de programador deve chamar o Adobe Pass **pré-autorizar** API com uma lista de IDs de recursos, que são uma sequência simples que geralmente representa um canal que um usuário pode ter direito a transmitir. *Observação: Atualmente, a variável* ***pré-autorizar*** *A chamada de é configurada para limitar a lista a cinco (5) IDs de recurso. Quando são necessários mais de cinco recursos, vários* ***pré-autorizar*** *As chamadas do podem ser feitas ou a chamada do pode ser configurada para aceitar mais de cinco recursos com um acordo dos MVPDs. Os implementadores devem ter em mente o custo de um* ***pré-autorizar*** *Chamar tanto os recursos do MVPD quanto o tempo de resposta ao Programador e estruturar seu uso da chamada de forma criteriosa.*

1. A variável **pré-autorizar** A chamada responderá ao Serviço do programador com um objeto JSON contendo um valor TRUE ou FALSE para cada ID de recurso na solicitação que indica se o usuário tem direito ao canal associado ou não. *Observação: Se um MVPD não fornecer uma resposta para um determinado ID de Recurso (por exemplo, devido a erros de rede ou timeouts), o valor assumirá FALSE como padrão.*

1. O Serviço de Programação deve utilizar o **pré-autorizar** Chamar a resposta para criar uma resposta personalizada definida pelo Programador para o Dispositivo de Streaming, normalmente para personalizar a apresentação ao usuário com base em suas autorizações.

O diagrama a seguir ilustra o fluxo de pré-autorização:

![](assets/preauthz-flow.png)


### \[Opcional\] Metadados

Os metadados podem ser usados para recuperar informações do usuário compartilhadas pelo MVPD.
 Exemplos disso podem incluir ID de usuário, código postal, etc.

1. Depois que o usuário é autenticado, o Serviço de programador pode chamar o Adobe Pass **metadados do usuário** API para solicitar informações sobre o usuário autenticado.

1. A resposta incluirá todos os metadados disponíveis para o usuário especificado. Os campos específicos são configurados separadamente para cada integração Programmer/MVPD.

O diagrama a seguir ilustra o fluxo de pré-autorização:

 

![](assets/user-metadata-api-preauthz.png)

 

## Ambientes e requisitos funcionais{#environments}

 

Um Programador deve criar pelo menos dois ambientes: um para produção e um ou mais para preparo.


### Produção

O ambiente de produção deve estar altamente disponível e dimensionado adequadamente para picos grandes ou inesperados (por exemplo, esportes ao vivo, notícias de última hora).

 

O serviço Adobe Pass é executado em vários data centers geograficamente dispersos nos EUA.  Para obter o melhor tempo de resposta (ou seja, a latência mais baixa) do serviço Adobe Pass, o programador também deve criar uma infraestrutura de serviço semelhante geograficamente dispersa. 


O serviço do Programador deve limitar o cache DNS a um máximo de 30s, caso o Adobe precise redirecionar o tráfego. Isso pode ocorrer se um data center se tornar indisponível.\
 

O Programador deve fornecer o intervalo de IP público do ambiente de produção. Eles serão inseridos em uma lista de permissões de IPs na infraestrutura do Adobe Pass para acesso e gerenciados pelas políticas de uso da API Adobe Fair.

### Estágios

O ambiente de preparo pode ser mínimo, mas deve incluir todos os componentes do sistema e a lógica de negócios. Ela deve funcionar de forma semelhante à produção e permitir o teste de versões fora da produção. Idealmente, o ambiente de preparo pode ser conectado aos ambientes de teste do Adobe Pass para uso do Programador e, quando necessário, por Adobe para que possamos ajudar no teste e na solução de problemas.

### Requisitos funcionais

O serviço Programador deve transmitir informações precisas de identificação do dispositivo para o qual está executando os fluxos. Além disso, o serviço Programador deve passar o IP do dispositivo para o qual está executando os fluxos (em um cabeçalho x-forwarded-for) junto com a porta de origem da conexão (no campo device info ):

    **X-Encaminhado-Para : \&lt;client _ip=&quot;&quot;>** 
    
    onde \&lt;client _ip=&quot;&quot;> é o endereço IP público do cliente
    
     
    
    O cabeçalho precisa ser adicionado às chamadas **regcode** e **authorize**
    
    Exemplos:
    
    POST /reggie/v1/{req\_id}/regcode HTTP/1.1
    
    X-Forwarded-For:203.45.101.20
    
     
    
    GET /api/v1/authorize HTTP/1.1
    
    X-Forwarded-For:203.45.101.20

 

O serviço Programador deve enviar dados e a formatação exigidos por MVPDs individuais ou aplicativos integrados (por exemplo, IP do dispositivo, porta de origem, informações do dispositivo, MRSS, dados opcionais, como ECID). <!--Please see the documentation for [Passing Device and Connection Information Cookbook](http://tve.helpdocsonline.com/passing-device-information-cookbook)-->.


O serviço Programador deve respeitar os TTLs authN e authZ ao armazenar em cache e invalidar as sessões authN ou authZ quando notificadas.

O Programador deve manter certificados compartilhados com o Adobe.

<!--
## Related Information {#related}

* [REST API Reference](/help/authentication/rest-api-reference.md)
* [Glossary of Terms](/help/authentication/adobe-pass-glossary.md)
-->
