---
title: Dynamic Client Registration Management
description: Dynamic Client Registration Management
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 0%

---


# Dynamic Client Registration Management {#dynamic-client-registration-management}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview}

Com a adoção generalizada de [Guias personalizadas do Android Chrome](https://developer.chrome.com/multidevice/android/customtabs){target_blanck} e [Controladora de visualização do Apple Safari](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target_blanck} nos aplicativos de nossos clientes, estamos atualizando o fluxo de autenticação de usuário na Autenticação Adobe Primetime. Mais especificamente, não podemos mais alcançar o objetivo de manter o estado para que o fluxo do agente do usuário de autenticação de um assinante MVPD possa ser rastreado entre redirecionamentos. Isso foi feito anteriormente usando cookies HTTP. Essa limitação é o driver para começar a migrar todas as APIs para o OAuth 2.0 [RFC6749](https://tools.ietf.org/html/rfc6749){target_blanck}.

Com esta atualização, os clientes de autenticação do Adobe tornam-se clientes OAuth 2.0 e um servidor de autorização OAuth 2.0 personalizado é implantado para atender às necessidades do Serviço de autenticação da Adobe Primetime.

Para que os aplicativos do cliente utilizem a autorização OAuth 2.0, o servidor deve se registrar dinamicamente para obter informações específicas (credenciais do cliente) para poder interagir com elas. Como parte do processo de registro, o cliente deve apresentar um conjunto de metadados incorporados ao endpoint de registro do cliente.

Esses metadados são comunicados como uma declaração de software, que contém um &quot;software_id&quot; para permitir que nosso servidor de autorização correlacione diferentes instâncias de um aplicativo usando a mesma declaração de software.

A **declaração de software** é um JSON Web Token (JWT) que afirma valores de metadados sobre o software cliente como um pacote. Quando apresentada ao servidor de autorização como parte de uma solicitação de registro de cliente, a declaração de software deve ser assinada digitalmente ou MACed usando JSON Web Signature (JWS).

Você pode encontrar uma explicação mais detalhada sobre o que são as declarações de software e como elas funcionam na documentação oficial [RFC7591](https://tools.ietf.org/html/rfc7591).

A declaração de software deve ser implantada com o aplicativo no dispositivo do usuário.

Antes dessa atualização, tínhamos dois mecanismos para permitir que aplicativos executassem chamadas para a autenticação da Adobe Primetime:

* clientes baseados em navegador são registrados por meio de permissão [listagem de domínios](/help/authentication/programmer-overview.md#reg-and-init)
* clientes de aplicativos nativos, como aplicativos iOS e Android, são registrados por meio de **solicitante assinado** mecanismo


Com o mecanismo de autorização Registro do cliente , você deve adicionar seus aplicativos ao painel TVE.

Para que um cliente comece a implementar o novo Android SDK e o próximo iOS SDK, ele precisa de uma declaração de software. Uma declaração de software identifica um aplicativo criado no Painel TVE.

Siga as etapas nas seções abaixo para criar um aplicativo registrado no painel TVE.

## Criar um aplicativo registrado {#create_app}

Há duas maneiras de criar um aplicativo registrado no painel TVE:

* [Nível do programador](#prog-level) - permite criar um Aplicativo Registrado e vinculá-lo a qualquer ou a todos os canais do Programador.

* [Nível de canal](#channel-level) - permite criar um Aplicativo Registrado que esteja vinculado permanentemente a este Canal sozinho.

### Criar um aplicativo registrado no nível do programador {#prog-level}

Ir para **Programadores** > **Aplicativos registrados** guia .

![](assets/reg-app-progr-level.png)

Na guia Aplicativos registrados , clique em **Adicionar novo aplicativo**. Preencha os campos obrigatórios na nova janela.

Conforme visto na imagem abaixo, os campos que você deve preencher são:

* **Nome do aplicativo** - o nome do pedido

* **Atribuído ao canal** - o nome do seu canal, t</span>ao qual este aplicativo está vinculado. A configuração padrão na máscara suspensa é **Todos os canais.** A interface permite selecionar um canal ou todos os canais.

* **Versão do aplicativo** - por padrão, está definido como &quot;1.0.0&quot;, mas recomendamos que você o modifique com sua própria versão do aplicativo. Como prática recomendada, se você decidir alterar a versão do aplicativo, reflita-a criando um novo aplicativo registrado para ele.

* **Plataformas de aplicativos** - as plataformas para o aplicativo a ser vinculado. Você tem a opção de selecionar todos ou vários valores.

* **Nomes de Domínio** - os domínios com os quais o aplicativo será vinculado. Os domínios na lista suspensa são uma seleção unificada de todos os domínios de todos os canais. Você tem a opção de selecionar vários domínios na lista. O significado dos domínios é URLs de redirecionamento [RFC6749](https://tools.ietf.org/html/rfc6749). No processo de registro do cliente, o aplicativo cliente pode solicitar a permissão para usar um URL de redirecionamento para a finalização do fluxo de autenticação. Quando um aplicativo cliente solicita um URL de redirecionamento específico, ele é validado em relação aos domínios da lista de permissões neste Aplicativo registrado associado à declaração de software.


![](assets/new-reg-app.png)


Depois de preencher os campos com valores apropriados, você deve clicar em &quot;Concluído&quot; para que o aplicativo seja salvo na configuração.

Esteja ciente de que **nenhuma opção para modificar um aplicativo já criado**. Caso se descubra que algo criado não atende mais aos requisitos , um novo aplicativo registrado precisará ser criado e usado com o aplicativo cliente cujos requisitos ele atende.


### Registrar um novo aplicativo no nível do canal {#channel-level}

Para criar um aplicativo registrado no nível do canal, navegue até o menu &quot;Canais&quot; e escolha aquele para o qual deseja criar um aplicativo. Em seguida, depois de navegar até a guia &quot;Aplicativos registrados&quot;, clique no botão &quot;Adicionar novo aplicativo&quot;.

![](assets/reg-new-app-channel-level.png)

Como mostrado abaixo, o que é um pouco diferente aqui , em comparação à mesma ação executada no nível do Programador, é a lista suspensa &quot;Canais atribuídos&quot; que não está ativada, portanto, não há opção para vincular o aplicativo registrado a outro canal.

![](assets/new-reg-app-channel.png)

## Listar aplicativos {#list-reg-app}

Depois de criar o aplicativo registrado, existe a possibilidade de obter uma declaração de software para apresentar o servidor de autorização como parte de uma solicitação.

Isso pode ser feito navegando até o Programador ou Canal para o qual os aplicativos registrados foram criados, onde estão listados. 

Como ilustrado abaixo , cada entrada na lista será identificada por um nome, versão e símbolos para plataformas às quais foi vinculada.

![](assets/reg-app-list.png)

Para cada um deles você pode :

* [Exibir](#view)
* [Baixar uma declaração de software](#download-statement)

### Visualizar um aplicativo registrado {#view}

Na lista de aplicativos, escolher um deles e clicar no botão &quot;Exibir&quot; mostrará os detalhes usados quando foi criado. Como mencionado anteriormente, não há opção para modificar nada.


![](assets/view-reg-app.png)


### Declaração de download de software {#download-statement}

Clicar no botão &quot;Download&quot; na entrada da lista para a qual uma instrução de software é necessária gerará um arquivo de texto. Esse arquivo conterá algo semelhante à saída de amostra abaixo.


![](assets/download-software-statement.png)

O nome do arquivo é identificado exclusivamente com a prefixação &quot;software_statement&quot; e a adição do carimbo de data e hora atual.

Observe que, para o mesmo aplicativo registrado, diferentes instruções de software serão recebidas sempre que o botão de download for clicado, mas isso não invalida as instruções de software obtidas anteriormente para esse aplicativo. Isso acontece porque elas são geradas no local, por solicitação de ação.

Há um **limitação** relacionado à ação de download. Se uma declaração de software for solicitada clicando no botão &quot;Download&quot; logo após a criação do aplicativo registrado e isso ainda não tiver sido salvo e a configuração json não tiver sido sincronizada, a seguinte mensagem de erro será exibida na parte inferior da página. 

![](assets/error-sw-statement-notready.png)

Isso envolve um código de erro HTTP 404 Not Found recebido do núcleo, pois a id do aplicativo registrado ainda não foi propagada e o núcleo não tem conhecimento dele.

A solução é, após criar o aplicativo registrado, aguardar no máximo 2 minutos para que a configuração seja sincronizada. Depois que isso acontecer, a mensagem de erro não será mais recebida e o arquivo de texto com a declaração de software estará disponível para download.

Para obter detalhes sobre como o processo de fim a fim funciona, ou para obter informações sobre como as solicitações são executadas e quais respostas esperar, consulte o link em Informações relacionadas abaixo, juntamente com outros links úteis.

<!--
## Related Information {#related}

* [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
* [TVE Dashboard User Guide](/help/authentication/tve-dashboard-user-guide.md)
-->

## Demonstração de recursos {#tutorial}

Observe [este webinário](https://my.adobeconnect.com/pzkp8ujrigg1/) O que fornece mais contexto dos recursos e contém uma demonstração sobre como gerenciar as instruções de software usando o painel TVE e como testar as geradas usando um aplicativo de demonstração fornecido pelo Adobe como parte do Android SDK.
