---
title: Visão geral para programadores
description: Visão geral para programadores
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4272'
ht-degree: 0%

---


# Visão Geral Para Programadores {#programmers-overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#introduction}

Esta visão geral destina-se ao provedor de conteúdo (Programador) que planeja integrar o Adobe® Pass em seu site ou aplicativo. Para obter a documentação adicional, incluindo o Kickstart e os guias de integração, consulte Informações relacionadas abaixo.

Hoje, seus visualizadores podem acessar a Internet a qualquer hora, em qualquer lugar, e solicitar acesso a conteúdo protegido diretamente de você, o Programador. Eles podem querer assistir a um evento único ou podem estar buscando direitos de exibição para uma série inteira de televisão que você está exibindo.

Mas antes de permitir o acesso ao seu conteúdo protegido, é necessário determinar se um cliente tem direito a visualizar esse conteúdo. Eles têm uma assinatura com um Distribuidor de programação de vídeo multicanal (MVPD)? Em caso afirmativo, essa assinatura inclui sua programação?

Determinar o direito de um visualizador nem sempre é simples para um programador. Os MVPDs mantêm os dados de identificação e os privilégios de acesso de seus clientes.  Adicione o fato de que os visualizadores que tentam acessar seu conteúdo protegido assinam uma variedade de MVPDs, cada um com sistemas diferentes, e é fácil ver que determinar o direito do visualizador ao conteúdo protegido pode se tornar rapidamente complicado e tecnicamente desafiador:

![](assets/user-ent-by-progr.png)

*Figura: Direito Do Usuário Determinado Diretamente Pelo Programador*

A autenticação Adobe Primetime para TV em qualquer lugar medirá com segurança essas transações de direito entre programadores e MVPDs. A autenticação da Adobe Primetime facilita, agiliza e protege os Programadores para fornecer conteúdo protegido a clientes válidos:

![](assets/user-ent-mediatedby-authn.png)

*Figura: Direitos de usuário mediados pela autenticação da Adobe Primetime*

A autenticação da Adobe Primetime atua como seu proxy em trocas com MVPDs participantes, para que você possa apresentar seus visualizadores com uma interface consistente entre sites. A autenticação da Adobe Primetime também permite fornecer aos visualizadores autenticação e autorização de logon único (SSO). A autenticação e a autorização são rastreadas para todos os serviços participantes, de modo que um assinante não precisa fazer logon novamente após sua primeira autenticação em seu próprio sistema.

* **Autenticação** - O processo de confirmação com um MVPD de que um determinado usuário é um cliente conhecido.
* **Autorização** - O processo de confirmação com um MVPD de que um usuário autenticado tem uma assinatura válida para um recurso especificado.

### Como a autenticação do Adobe Primetime funciona {#HowItWorks}

O aplicativo de visualização de conteúdo do Programador interage com a autenticação da Adobe Primetime usando o componente do cliente Ativador de Acesso ou os serviços Web RESTful da API sem cliente (para dispositivos sem capacidade para a Web, como TVs inteligentes, consoles de jogos, conversores de sinais, etc.). O Ativador de Acesso é executado no sistema do usuário, onde facilita todos os workflows de direito.  O componente Ativador de acesso é baixado de seu site de hospedagem no Adobe, quando os clientes acessam seu site e solicitam conteúdo protegido.  Os servidores de autenticação da Adobe Primetime hospedam os serviços Web RESTful usados na solução sem cliente.

A autenticação da Adobe Primetime lida com os workflows de direito reais e, ao mesmo tempo, fornece primitivos usados para:

* Defina sua identidade. (O Programador é o &quot;solicitante&quot; no fluxo de direito de autenticação da Adobe Primetime.)
* Autentique um usuário com um MVPD específico.  (O MVPD é o &quot;provedor de identidade&quot; ou &quot;IdP&quot; no fluxo de direito de autenticação da Adobe Primetime.)
* Autorize um usuário com o MVPD para um recurso específico.
* Faça logout do usuário.

O Programador é responsável por sua página da Web de nível superior ou aplicativo do player que faz o seguinte:

* Implementa a interface do usuário
* Interage com os serviços da Web do Access Enabler ou da API sem cliente

O objetivo da autenticação da Adobe Primetime é criar uma maneira simples e modular para Programadores e MVPDs lidarem com a verificação de direito.

## Noções básicas sobre tokens {#understanding-tokens}

A solução de direito de autenticação da Adobe Primetime se concentra na geração de partes específicas de dados criadas após a conclusão com êxito dos workflows de autenticação e autorização. Esses dados são chamados de tokens. Os tokens têm uma duração limitada; quando expiram, os tokens precisam ser reemitidos por meio do reinício dos fluxos de trabalho de autenticação e autorização.

Para obter detalhes sobre tokens, consulte as seguintes seções:

* [Tipos de tokens](#token-types)
* [Armazenamento de tokens](#token-storage)
* [Segurança de token](#token-security)
* [Compartilhamento de token](#token-sharing)

### Tipos de tokens {#token-types}

Três tipos de tokens são emitidos durante os fluxos de trabalho de autenticação e autorização. Os tokens AuthN e AuthZ têm &quot;vida longa&quot;, proporcionando continuidade à experiência de visualização do usuário. O Media Token é um token de curta duração que fornece suporte para as práticas recomendadas do setor, a fim de evitar fraudes por meio de ripagem. Os programadores especificam os valores de TTL (time-to-live) para cada tipo de token com base em acordos feitos com MVPDs. Os programadores decidem sobre um valor de TTL que melhor atende à sua empresa e aos seus clientes.

* **Token de AuthN** (&quot;Vida longa&quot;): Após a autenticação bem-sucedida, a autenticação da Adobe Primetime cria um token AuthN associado ao dispositivo solicitante e um GUID (identificador globalmente exclusivo).
   * A autenticação da Adobe Primetime envia o token AuthN para o Criador de acesso, que o armazena em cache com segurança no sistema do cliente.  Embora o token AuthN esteja lá e ainda não tenha expirado, ele está disponível para todos os aplicativos que usam a autenticação Adobe Primetime. O Ativador de acesso usa o token AuthN para o fluxo de autorização.
   * Em um determinado momento, apenas um token AuthN é armazenado em cache. Sempre que um novo token AuthN for emitido e um antigo já existir, a autenticação do Adobe Primetime substituirá o token em cache.
* **Token de AuthZ** (&quot;Vida longa&quot;): Após uma autorização bem-sucedida, a autenticação do Adobe Primetime cria um token AuthZ associado ao dispositivo solicitante e a um recurso protegido específico.  O recurso protegido é identificado por uma ID de recurso exclusiva.
   * A autenticação da Adobe Primetime envia o token AuthZ para o Ativador de acesso, que o armazena em cache com segurança no sistema local. O Ativador de acesso usa o token AuthZ para criar o token de mídia de curta duração usado para o acesso de visualização real.
   * Em qualquer momento, apenas um token AuthZ por recurso é armazenado em cache. A autenticação da Adobe Primetime pode armazenar em cache vários tokens AuthZ, desde que associados a recursos diferentes. Sempre que um novo token AuthZ é emitido e um antigo já existe para o mesmo recurso, a autenticação do Adobe Primetime substitui o token em cache.
* **Token de mídia** (&quot;Short-Lived&quot;): O Ativador de acesso usa o token AuthZ para gerar uma vida curta (padrão: 7 minutos) Token de mídia. Este é o ponto em que se considera ter ocorrido um pedido de reprodução bem-sucedido.
   * Antes de fornecer acesso ao recurso protegido, o servidor de mídia deve usar um componente de autenticação da Adobe Primetime, o Verificador de token de mídia, para validar o token de mídia.
   * Como o token de mídia não está vinculado ao dispositivo, sua duração é significativamente menor (padrão: 7 minutos) mais do que os tokens AuthN e AuthZ de vida longa.
   * O token de mídia de curta duração é restrito ao uso único e nunca é armazenado em cache. Ele é recuperado do servidor de autenticação da Adobe Primetime sempre que uma API de autorização é chamada.

### Armazenamento de tokens {#token-storage}

O Access Enabler armazena tokens de longa duração (AuthN e AuthZ) em locais específicos ao seu ambiente:

* **Flash 10.1** (ou superior): Os tokens de vida longa são armazenados como Objetos compartilhados locais.
* **HTML5**: Os tokens de longa duração são mantidos em segurança na loja local do navegador HTML5.
* **iOS**: Os tokens de longa duração são armazenados em uma área de transferência persistente, onde podem ser acessados por outros aplicativos clientes de autenticação da Adobe Primetime.
* **Android**: Os tokens de duração são armazenados em um arquivo de banco de dados compartilhado, onde podem ser acessados por outros aplicativos clientes de autenticação da Adobe Primetime.
* **Dispositivos de API sem cliente**: Os tokens são armazenados nos servidores de autenticação do Primetime.

### Segurança de token {#token-security}

O Servidor de autenticação da Adobe Primetime assina digitalmente todos os tokens de longa duração usando a ID do dispositivo (derivada das características de hardware do dispositivo). A assinatura digital difere na forma como é gerada, protegida e validada, dependendo do ambiente:

* **Flash 10.1** (ou superior) - A ID do dispositivo depende da credencial do dispositivo, um certificado exclusivo emitido do servidor de individualização do Adobe. Essa segurança é equivalente à tecnologia FAXS DRM. Essa validação do lado do servidor compara a ID de dispositivo exclusiva no token com a credencial do dispositivo (comunicada com segurança do Flash Player para a autenticação da Adobe Primetime). A credencial do dispositivo também identifica a versão do cliente FAXS e a versão do Flash Player (ou AIR) para a qual foi emitida. A vinculação do dispositivo é mais forte do que com a HTML5, portanto, o TTL (time-to-live) para os tokens geralmente é maior com o Flash.
* **HTML5** - O dispositivo é individualizado no lado do cliente. Ela usa características disponíveis no JavaScript para produzir uma ID de pseudodispositivo que inclui versões de navegador e SO, um endereço IP e um GUID de cookie do navegador (identificador globalmente exclusivo). Essa ID de dispositivo de token é comparada à ID de pseudo-dispositivo atual do dispositivo. Como o endereço IP pode mudar durante o uso normal, mesmo na mesma sessão, a autenticação da Adobe Primetime armazena os tokens de HTML5 em dois locais: localStorage e sessionStorage. Se o IP mudar e o token sessionStorage ainda for válido, a sessão será mantida. Com a HTML5, a vinculação do dispositivo não é tão forte, portanto, o TTL para tokens normalmente é menor do que para o Flash.
* **Clientes nativos** (iOS e Android) - Os tokens de longa duração contêm informações de individualização da ID do dispositivo nativa e, portanto, estão vinculados ao dispositivo solicitante. As solicitações de autenticação e autorização são enviadas por HTTPS, e as informações da ID do dispositivo são assinadas digitalmente pela biblioteca do Ativador de Acesso antes de enviá-las para os servidores de backend. No lado do servidor, as informações da ID do dispositivo são validadas em relação à assinatura digital associada.
* **Clientes de API sem cliente** - A solução de API sem cliente tem seu conjunto de protocolos de segurança que envolvem a assinatura digital de todas as chamadas de API. Os tokens gerados durante os fluxos de direito são armazenados com segurança nos servidores de autenticação da Adobe Primetime.

A autenticação da Adobe Primetime valida cada token de duração longa para garantir que o dispositivo que acessar o conteúdo seja o mesmo que o que emitiu o token. Para todos os tokens, uma validação do lado do cliente garante que a assinatura digital esteja intacta e que a integridade do token seja preservada. Quando a validação da ID do dispositivo falhar, a sessão de autenticação será invalidada e o usuário será solicitado a fazer logon novamente, o que redefinirá os tokens.

### Compartilhamento de token {#token-sharing}

Aplicativos em plataformas diferentes não compartilham tokens. Existem vários motivos para isso, incluindo o seguinte:

* Conforme descrito em [Armazenamento de tokens](#token-storage), o método de armazenamento de tokens varia entre plataformas (por exemplo, Objetos compartilhados locais para Flash, WebStorage para JavaScript).
* O grau de segurança do token é diferente entre plataformas. Por exemplo, os tokens de Flash são fortemente vinculados a um dispositivo que usa o FAXS. Os tokens em um ambiente JavaScript puro não têm o mesmo nível de suporte de DRM que o Flash.  O compartilhamento de tokens JS com aplicativos Flash aumentaria a possibilidade de tokens menos seguros explorarem um ambiente mais seguro.

## Ciclo de vida da integração do programador {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*Figura: Integração da autenticação com o site e o aplicativo do programador*


## Fluxos lógicos {#logical-flows}

### Fluxograma de direitos {#chart}

O fluxograma a seguir apresenta o processo geral de confirmação do direito (usando o componente cliente Adobe Primetime authentication Access Enabler ):

![](assets/ent-flowchart.png)

*Figura: Processo de confirmação do direito*

### Etapas de autenticação {#authn-steps}

As etapas a seguir apresentam um exemplo do fluxo de autenticação da Adobe Primetime.  Essa é a parte do processo de direito no qual um Programador determina se o usuário é um cliente válido de um MVPD.  Nesse cenário, o usuário é um assinante válido de um MVPD.  O usuário está tentando visualizar conteúdo protegido usando um aplicativo Flash do Programador:

1. O usuário navega até a página da Web do Programador, que carrega o aplicativo do Flash do Programador e os componentes do Ativador de acesso para autenticação da Adobe Primetime na máquina do usuário. O aplicativo Flash usa o Ativador de Acesso para definir a identificação do Programador com autenticação Adobe Primetime, e a autenticação Adobe Primetime prioriza o Ativador de Acesso com dados de configuração e estado para esse Programador (o &quot;solicitante&quot;). O Ativador de acesso deve receber esses dados do servidor antes de executar qualquer outra chamada de API. Nota técnica: o Programador definiu sua identidade com o Enabler de Acesso `setRequestor()` método; para obter detalhes, consulte o [Guia de integração do programador](/help/authentication/programmer-integration-guide-overview.md).
1. Quando o usuário tenta visualizar o conteúdo protegido do Programador, o aplicativo do Programador apresenta ao usuário uma lista de MVPDs, a partir da qual o usuário seleciona um provedor.
1. O usuário é redirecionado para um servidor de autenticação da Adobe Primetime, onde um [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) A solicitação para o MVPD selecionado pelo usuário é criada. Esta solicitação é enviada como uma solicitação de autenticação em nome do Programador para o MVPD. Dependendo do sistema do MVPD, o navegador do usuário é redirecionado para o site do MVPD para fazer logon ou um iFrame de login é criado no aplicativo do Programador.
1. Em ambos os casos (redirecionamento ou iFrame), o MVPD aceita a solicitação e exibe sua página de logon.
1. O usuário faz logon com o MVPD, o MVPD valida o status do usuário como um cliente pagador e, em seguida, o MVPD cria sua própria sessão HTTP.
1. Quando o usuário é validado, o MVPD cria uma resposta (SAML &amp; criptografada), que o MVPD envia de volta para a autenticação da Adobe Primetime.
1. A autenticação Adobe Primetime recebe a resposta MVPD, vê que há uma sessão HTTP de autenticação Adobe Primetime aberta, valida a resposta SAML do MVPD e redireciona para o site do Programador.
1. O site do Programador é recarregado, o Ativador de Acesso é recarregado e o Programador chama setRequestor() novamente.  A segunda chamada para setRequestor() é necessária porque a configuração atual foi alterada - agora há um sinalizador presente que informa ao Ativador de Acesso que um token AuthN está aguardando ser gerado no servidor.
1. O Ativador de Acesso vê que há uma autenticação pendente e solicita o token do servidor de autenticação da Adobe Primetime. O token é recuperado do servidor, chamando os recursos de DRM do Flash Player.
1. O token AuthN é armazenado no cache LSO do Flash Player do programador; a autenticação agora é concluída e a sessão é destruída no servidor de autenticação da Adobe Primetime.

### Etapas de autorização {#authz-steps}

As etapas a seguir continuam do [Etapas de autenticação](#authn-steps):

1. Quando o usuário tenta acessar o conteúdo protegido do Programador, o aplicativo do Programador verifica primeiro se há um token AuthN no computador ou dispositivo local do usuário.  Se esse token não estiver lá, então a variável [Etapas de autenticação](#authn-steps) acima são seguidas.  Se o token AuthN estiver lá, o fluxo de Autorização continuará com o aplicativo do Programador iniciando uma chamada para o Criador de Acesso com uma solicitação para obter os direitos de visualização do usuário para um item específico de conteúdo protegido.
1. O item específico de conteúdo protegido é representado por um &quot;identificador de recurso&quot;.  Pode ser uma sequência simples ou uma estrutura mais complexa, mas em qualquer caso a natureza do identificador de recursos é acordada antecipadamente entre o programador e o MVPD.  O aplicativo do Programador passa o identificador de recurso para o Ativador de Acesso.  O Ativador de Acesso verifica se há um token AuthZ no computador ou dispositivo local do usuário.  Se o token AuthZ não estiver lá, o Habilitador de acesso passará a solicitação para o servidor de autenticação da Adobe Primetime de back-end.
1. O servidor de autenticação da Adobe Primetime se comunica com o endpoint de autorização MVPDs usando protocolos padronizados.  Se a resposta do MVPD indicar que o usuário tem direito a exibir o conteúdo protegido, o servidor de autenticação da Adobe Primetime cria um token AuthZ e o transmite para o Ativador de acesso, que armazena o token AuthZ na máquina do usuário.
1. Com um token AuthZ armazenado no computador ou no dispositivo do usuário, o aplicativo Programador chama o Criador de acesso para obter um Token de mídia do servidor de autenticação da Adobe Primetime e fornece esse token para o aplicativo do Programador.
1. Por fim, o aplicativo do Programador usa o componente Verificador de token de mídia para confirmar que o usuário correto está visualizando o conteúdo correto, e com o Token de mídia no lugar, o usuário tem permissão para visualizar o conteúdo protegido.


## Registro e inicialização {#reg-and-init}

A primeira etapa para trabalhar com a autenticação da Adobe Primetime é se registrar no Adobe ou com um parceiro autorizado para autenticação da Adobe Primetime.

Ao se registrar, você fornece uma lista dos domínios dos quais se comunicará com a autenticação da Adobe Primetime. Por exemplo, os domínios Turner Broadcasting System incluem tbs.com e tnt.tv como domínios registrados pela autenticação da Adobe Primetime. Cada um desses sites de conteúdo recebe acesso à autenticação da Adobe Primetime e recebe sua própria ID de Solicitante (por exemplo, &quot;TBS&quot; e &quot;TNT&quot;). Se decidir adicionar outros sites, você deve informar o Adobe sobre os nomes de domínio adicionais para colocá-los na lista de domínios permitidos e receber IDs de Solicitante adicionais.

>[!WARNING]
>
>Ao testar sua integração, verifique se o servidor de teste está em um domínio registrado que você pretende usar na produção. As solicitações, mesmo as solicitações de teste, provenientes de domínios não incluídos na lista de permissões são ignoradas. Por exemplo, se você solicitou que domain.com fosse usado na produção, verifique se está implantando sua integração de teste em domain.com, test.domain.com e staging.domain.com.
>
>As solicitações que contêm nome de usuário e/ou senha no URL são ignoradas mesmo se os domínios forem incluídos na lista de permissões. Exemplo: `//username@registered-domain/`

A ID do Solicitante identifica exclusivamente o cliente do Programador em todas as comunicações com o componente do cliente Ativador de Acesso da Adobe Primetime. Todos os dados estáticos de autenticação do Adobe Primetime associados ao Programador são marcados com essa ID.

>[!TIP]
>
>Além da ID do Solicitante, ao se registrar, você também receberá URLs funcionais para o componente do cliente Ativador de Acesso e o Verificador de Token de Mídia.

## Etapas de integração {#integration-steps}

>[!TIP]
>
>Se você estiver usando o Open Source Media Framework do Adobe (&quot;OSMF&quot;) para o desenvolvimento de sua mídia, a maneira mais rápida de usar a autenticação do Adobe Primetime é integrar o plug-in OSMF *(Obsoleto)* no código do seu jogador.
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [Configuração do solicitante](#requestor)
1. [Manipular autenticação e autorização](#authn-authz)
1. [Suporte ao Logout Único](#ssl)

### 1. Configuração do solicitante {#requestor}

#### 1 bis. Registrando-se com o Adobe

Sua primeira etapa é se registrar no Adobe ou com um parceiro autorizado de autenticação da Adobe Primetime.  Ao se registrar, você recebe um ou mais identificadores globais exclusivos (GUIDs). Cada GUID emitida está associada a um domínio do qual o acesso é permitido para a autenticação da Adobe Primetime. Você passa um GUID (chamado de ID do solicitante) para o domínio que fez a solicitação para registrar sua identidade para cada sessão em que interage com o Ativador de acesso. Para obter detalhes, consulte [Registro e inicialização](#reg-and-init) no Guia de integração do programador.

#### 1-B. Integração do ativador de acesso inicial

A próxima etapa é integrar o Ativador de acesso ao aplicativo do reprodutor de mídia ou página da Web existente:

* Você pode incorporar a versão do Flash, `AccessEnabler.swf`, em um reprodutor de vídeo baseado em Flash, ou você pode incorporá-lo diretamente ao HTML da página da Web. Você pode se comunicar com o SWF Access Enabler no ActionScript ou no JavaScript. A API base é o ActionScript, mas se você preferir trabalhar com JavaScript, uma biblioteca de wrapper completa estará disponível para inclusão em suas páginas.
* Para ambientes que não sejam Flashes, você pode:
   * Use a versão HTML5/JavaScript, AccessEnabler.js e comunique-se com ela por meio da API do JavaScript
   * Use a Extensão nativa do AIR para autenticação do Adobe Primetime para combinar o código nativo com classes de ActionScript integradas
   * Usar uma das versões nativas do cliente da biblioteca do Access Enabler (iOS ou Android)

### 2. Manipulação da autenticação e da autorização {#authn-authz}

#### 2 bis. Comunicação com o ativador de acesso

A comunicação entre o Ativador de acesso e a página da Web ou o aplicativo do reprodutor é assíncrona. Seu aplicativo chama métodos do Access Enabler e o Access Enabler responde por meio de retornos de chamada que você registra na biblioteca do Access Enabler.

* Quando seu aplicativo faz uma solicitação de autorização, o Ativador de Acesso inicia automaticamente uma solicitação de autenticação, se um token AuthN válido ainda não estiver no sistema local. Quando a autenticação é bem-sucedida, o token AuthN do usuário é armazenado localmente, de modo que não é necessário fazer logon novamente. Se eles tiverem sido autenticados com êxito por meio da autenticação da Adobe Primetime em qualquer outro contexto (por exemplo, por meio do site do MVPD ou com um programador diferente), o Ativador de acesso terá acesso ao token AuthN local e uma autenticação adicional não será necessária.
* Quando um usuário tenta acessar seu conteúdo protegido, você envia uma solicitação de autorização ao Ativador de acesso. Após verificar (ou iniciar) a autenticação, o Habilitador de Acesso entra em contato com o MVPD (por meio do servidor de autenticação da Adobe Primetime) para determinar se o cliente tem direito a exibir o conteúdo protegido. Seu aplicativo só precisa enviar a solicitação ao Enabler de acesso e, em seguida, lidar com a resposta (sucesso ou falha da autorização). Se a autorização for bem-sucedida, um token AuthZ será armazenado no sistema cliente.  Por fim, seu aplicativo recebe um token de mídia de curta duração para uso em seu próprio procedimento de autorização.

>[!NOTE]
>
>* A autenticação ocorre como uma troca SAML, entre a autenticação Adobe Primetime como Provedor de Serviços (SP) e o MVPD como Provedor de Identidade (IdP).
>
>* A autorização usa uma troca de serviço da Web de canal reverso (servidor para servidor) entre a autenticação da Adobe Primetime (o SP) e um MVPD (o IdP).



#### 2 ter. Fornecendo Uma Interface De Usuário De Direito {#entitlement-ui}

Você fornece sua própria interface do usuário para acessar seu conteúdo. Alguns elementos, como o processo de logon real, são fornecidos pelo MVPD e alguns elementos estão opcionalmente disponíveis como parte da autenticação da Adobe Primetime. No mínimo, você faz o seguinte:

* **Implemente uma interface de seleção MVPD que permita que um novo usuário identifique seu MVPD e faça logon pela primeira vez**. Para desenvolvimento, o Ativador de acesso fornece uma interface de usuário básica que dá ao cliente uma opção de MVPDs e inicia o processo de logon. Para produção, você deve implementar sua própria caixa de diálogo Seletor de MVPD. Alguns MVPDs redirecionam para seu próprio site para logon e alguns exigem que suas páginas de logon sejam exibidas em um iFrame. Você deve implementar um retorno de chamada que crie este iFrame para lidar com os casos em que o MVPD do usuário exibe sua página de logon em um iFrame.
* **Identificar conteúdo protegido**. O conteúdo protegido requer autorização para acessar o . Sua interface deve indicar qual conteúdo está protegido e qual conteúdo foi autorizado.  O status da autorização é frequentemente indicado com ícones &quot;desbloqueados&quot; e &quot;bloqueados&quot;.
* **Mostrar que um usuário está autenticado**. Você deve indicar o status de autenticação de um usuário como parte de qualquer meio usado para identificar conteúdo protegido. Você pode consultar o Ativador de acesso para determinar se o cliente já foi autenticado.

#### 2-C. Integração do verificador de token de mídia {#int-media-token-ver}

Você deve integrar o componente Verificador de token de mídia de autenticação da Adobe Primetime ao seu servidor de mídia.  Assim, seu verificador de token existente pode reconhecer os tokens de mídia de curta duração fornecidos pela autenticação da Adobe Primetime com uma autorização bem-sucedida. O Verificador de token de mídia valida os tokens de mídia como a última etapa de segurança antes de fornecer ao usuário acesso a conteúdo protegido. Você recebe o local do qual deseja baixar o Verificador de token de mídia ao se registrar no Adobe.

### 3. Suporte ao Logout Único {#ssl}

Na maioria dos casos, o reprodutor de mídia é responsável por gerenciar logouts de usuário por meio de uma API de habilitação de acesso simples. Quando você chama logout(), o Ativador de acesso faz o seguinte:

* Faz logoff do usuário atual
* Limpa todas as informações de autenticação e autorização do usuário desconectado
* Exclui todos os tokens AuthN e AuthZ do sistema local do usuário

Se o usuário deixar a máquina ociosa por tempo suficiente para que os tokens expirem, ele ainda poderá retornar à sessão e iniciar o logout com êxito. A autenticação da Adobe Primetime garante que todos os tokens sejam excluídos e notifica o MVPD para excluir sua sessão também.

Quando o logout é iniciado a partir de um site que não está integrado à autenticação da Adobe Primetime, o MVPD pode chamar o serviço de Logout Único de autenticação da Adobe Primetime por meio de um redirecionamento do navegador.

## Como entender IDs de usuário {#user-ids}

Conceitualmente, cada usuário que inicia um fluxo de direito é associado a uma única ID de usuário exclusiva.  No entanto, durante um fluxo de direito, essa ID de usuário pode ser apresentada de diferentes maneiras, dependendo da API da qual você obtém a ID.

O sessionGUID no Token de mídia curta é a forma segura do UserID, que está disponível por meio da chamada sendTrackingData() .   Em todas as integrações atuais, esse é um GUID persistente para o usuário ao longo do tempo e dos dispositivos, mas a fonte do GUID começa com o UserID na resposta SAML do MVPD.   No entanto, alguns MVPDs podem mudar de ideia no futuro e começar a enviar um GUID transitório.  Se um Programador quiser garantir que o UserID de origem do MVPD na resposta do AuthN seja persistente, ele deverá providenciar isso em seus contratos com MVPDs.

Estas são as diferentes maneiras em que a ID de usuário é representada nas APIs de autenticação do Adobe Primetime:

* `sendTrackingData()` Propriedade GUID - Esta é a versão com hash do Adobe do UserID do MVPD.  Ele tem hash para que essa ID de usuário não possa ser rastreada de volta para a fonte do MVPD.   Essa ID é exclusiva e normalmente persistente, mas não pode ser compartilhada com o MVPD para comparar o comportamento de uso específico com o que os MVPDs têm no seu lado.   Não está assinado digitalmente, portanto não é infalível para a prevenção da fraude, mas é suficientemente bom para a análise.  Esse formulário da ID de usuário é fornecido no lado do cliente em todos os eventos gerados pela autenticação da Adobe Primetime no fluxo AuthN/AuthZ.
* Token de mídia curta `sessionGUID` propriedade - É o mesmo que UserID via `sendTrackingData()`, no entanto, este é assinado digitalmente para proteger sua integridade.  Isso torna esse valor bom o suficiente para rastrear fraudes de uso simultâneo. Ele deve ser processado no lado do servidor após o uso da biblioteca do validador e pode ser analisado em busca de padrões de fraude antes de lançar o fluxo de vídeo para o cliente.  Fazer qualquer uma dessas tarefas depende do Programador.
* `getMetadata() userID `propriedade - Essa propriedade permitirá que o Adobe exponha a ID de usuário MVPD de origem real ao Programador. Ele será criptografado com a chave pública pelo certificado que temos do Programador, para que não seja exposto de forma clara ao cliente. Isso fornece ao Programador o UserID real do MVPD, então é algo que pode ser usado para vinculação de contas ou investigação de fraude diretamente com o MVPD.

**Em conclusão**

* A ID de usuário do MVPD é uma ID exclusiva persistente, embora não garantida, geralmente **gerado a partir dos MVPDs e passado para o Adobe na autenticação bem-sucedida**. Geralmente é consistente em todas as redes, com algumas exceções.
* A ID de usuário do MVPD não contém PII e NÃO é um número de conta. Ele não precisa ser exposto em um formulário criptografado, pois validamos com todos os MVPDs que nenhum PII está sendo enviado.


A forma como você usa a ID do usuário depende do caso de uso:

* Se for necessário para rastreamento/análise, o local mais prático é obtê-la de `sendTrackingData()`.
* Se precisar deles no lado do servidor para liberação de fluxo, fraude ou dados operacionais, você pode obtê-los do Validador de token de mídia.
* Se precisar disso para vinculação de contas e fraude mais profunda, verifique sua disponibilidade com o Adobe contact.

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->