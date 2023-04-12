---
title: Visão geral para MVPDs
description: Visão geral para MVPDs
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---


# Uma visão geral dos MVPDs {#mvpd-overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#intro}

Esta visão geral é destinada aos Distribuidores de Programação de Vídeo de Vários Canais (MVPDs). Para obter a documentação adicional, incluindo o Kickstart e os guias de integração, consulte a seção Informações relacionadas no final deste documento.



A TV em qualquer lugar (TVE) é o movimento do setor, já bem conhecido, que permite que assinantes de TV paga acessem o conteúdo que já pagam, em vários dispositivos, dentro e fora de suas casas.  Para provedores de TV paga, o TVE cria novas oportunidades, tanto para preservar os relacionamentos existentes com os clientes quanto para permitir novos. No entanto, juntamente com estas oportunidades surgem desafios. No cenário TVE, Programadores fornecem o conteúdo, mas os MVPDs mantêm as informações do cliente para verificar se visualizadores em potencial são assinantes válidos.



Coordenar a autenticação e a autorização do visualizador com um programador pode ser simples, mas coordenar com dezenas ou centenas de programadores diferentes torna-se cada vez mais complexo. No entanto, com o Adobe® Pass, os MVPDs só precisam implementar uma integração simples e única para obter acesso a todo o ecossistema TVE, incluindo programadores como NBCUniversal Media, Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks, Hulu e assim por diante.  A autenticação da Adobe Primetime fornece uma estrutura de integração que torna a determinação do direito do usuário simples e segura.



Fim da linha: A autenticação da Adobe Primetime medirá com segurança as transações de direito entre Programadores e MVPDs, facilitando o acesso do visualizador ao conteúdo da assinatura. Em outras palavras, a autenticação da Adobe Primetime facilita e agiliza o acesso dos clientes certos ao conteúdo correto.


Com a autenticação da Adobe Primetime, os MVPDs recebem:

Integração fácil com programadores.  Ofereça conectividade instantânea de vários proprietários de conteúdo com uma única integração.

Engajamento aprimorado com o cliente.  Oferece suporte a uma experiência perfeita e com a marca à medida que seus clientes visualizam o conteúdo em várias plataformas e dispositivos.

Autenticação segura.  Certifique-se de que somente usuários e dispositivos autorizados tenham acesso a conteúdo premium e (opcionalmente) limite o número de dispositivos e fluxos simultâneos que podem se conectar por conta doméstica.

## Perguntas frequentes {#faq}

Qual é a segurança da autenticação da Adobe Primetime? A prioridade número um da arquitetura de autenticação da Adobe Primetime é garantir que somente os visualizadores autorizados sejam autenticados e tenham acesso ao conteúdo premium. A autenticação da Adobe Primetime vincula o acesso aos dispositivos de visualização e pode ajudar a limitar fluxos, sessões e/ou dispositivos de uma determinada família.


O Flash Player é necessário? Autenticação Adobe Primetime para TV em qualquer lugar é independente de player e plataforma, integrando-se a qualquer aplicativo de reprodução, incluindo Silverlight e HTML5. Além disso, a autenticação da Adobe Primetime fornece suporte nativo para dispositivos como telefones e tablets que executam iOS e Android.


Quais dispositivos são compatíveis com a autenticação da Adobe Primetime? A autenticação do Adobe Primetime é compatível com praticamente qualquer dispositivo com o kit da Web HTML5 para experiências de visualização no navegador. Além disso, a autenticação da Adobe Primetime continua a implantar SDKs (Kits de desenvolvimento de software) nativos para várias plataformas específicas de dispositivos, incluindo aplicativos iOS, Android™, Xbox360 (obsoleto) e Adobe Air® (obsoleto). Mais recentemente, a autenticação da Adobe Primetime lançou uma solução sem cliente para dispositivos que não podem renderizar páginas do navegador (por exemplo, TVs &quot;inteligentes&quot;, decodificadores de sinais e consoles de jogos).  A capacidade de renderizar páginas do navegador é um requisito para a autenticação de usuários com MVPDs.


A autenticação da Adobe Primetime é compatível com os padrões emergentes para TV em qualquer lugar? A autenticação da Adobe Primetime é compatível com a especificação CableLabs OLCA (Online Content Access), que fornece requisitos técnicos e arquitetura para a entrega de vídeo a um cliente de TV paga de fontes online. A Adobe participou do projeto conjunto de testes interopcionais CableLabs em junho de 2011 e aprovou o processo de teste para a implementação de um Provedor de serviços. A autenticação da Adobe Primetime é verificada (concluída e testada) em relação às especificações OLCA para autenticação. O componente de autorização é concluído, mas a verificação de teste aguarda atualmente a liberação do ambiente de teste do CableLabs. O Adobe é também membro ativo do OATC (Open Authentication Technical Consortium) e participa em vários projetos de especificação dos subcomités como parte desse organismo.



O que é Autenticação? Autenticação é o processo em que um MVPD confirma que um determinado usuário é um cliente conhecido.



O que é autorização? Autorização é o processo no qual um MVPD confirma que um usuário autenticado tem uma assinatura válida para um determinado recurso.



## Arquitetura {#architecture}

A autenticação da Adobe Primetime é um serviço hospedado que permite a integração rápida de back-end (servidor para servidor) com base nas regras de negócios exigidas pelos MVPDs e Programadores. Isso significa um tempo rápido para comercializar para todas as partes, um ambiente mais seguro para evitar fraudes e uma experiência superior do cliente, com mais conteúdo de TV disponível para mais pessoas em mais plataformas.


A autenticação da Adobe Primetime é oferecida por meio do modelo Software as a Service (SaaS) e permite que uma comunicação mais segura ocorra entre usuários finais, MVPDs e Programadores, a fim de validar o direito ao conteúdo. Os componentes principais do serviço incluem:

Lado do servidor - O servidor de autenticação da Adobe Primetime hospedado. Este é um servidor de aplicativos que faz a comunicação de canal traseiro (servidor para servidor) com os sistemas de autenticação de MVPDs.
Lado do cliente: O ativador de acesso do lado do cliente - o ativador de acesso é um pequeno arquivo carregado na página da Web ou aplicativo do player de um programador. Ele fornece APIs de direito ao aplicativo de visualização de conteúdo do Programador e se comunica com o Servidor de autenticação da Adobe Primetime.
Serviços Web sem cliente (para dispositivos que não são compatíveis com a Web) - Serviços Web RESTful que fornecem APIs de direito para dispositivos como TVs inteligentes, consoles de jogos e decodificadores de sinais.

>[!NOTE]
>
>Como um MVPD, seus serviços da Web devem ser capazes de reconhecer solicitações de autenticação e autorização da autenticação da Adobe Primetime e responder com os dados necessários no formato esperado.

A autenticação da Adobe Primetime permite fornecer aos clientes gerenciamento de identidade federado, também conhecido como autenticação e autorização de logon único (SSO). Com a autenticação da Adobe Primetime, não há necessidade de os assinantes fazerem logon novamente após sua primeira autenticação, desde que essa autenticação seja permitida pelo MVPD para persistir. (Normalmente, 30 dias.) Para isso, a autenticação da Adobe Primetime fornece um domínio comum para tokens de autenticação para nossos clientes. Essas informações de estado de autenticação estão disponíveis para todos os sites participantes integrados a um determinado MVPD.


Atualmente, a maioria das integrações de autenticação da Adobe Primetime com MVPDs usa o protocolo SAML, um dos padrões de autenticação primários. A autenticação da Adobe Primetime atua como um Provedor de serviços proxy na arquitetura SAML e persiste a resposta de autenticação SAML como um token seguro no domínio Adobe common. A autenticação da Adobe Primetime é compatível com SAML 2.0. No entanto, embora a autenticação da Adobe Primetime seja normalmente usada com soluções SAML SSO neste ponto, a arquitetura de autenticação da Adobe Primetime não está vinculada a nenhum protocolo específico. Portanto, o suporte para novos protocolos - como um baseado no OAuth 2.0 ou em protocolos personalizados - pode ser adicionado ao longo do tempo.


O Adobe funciona com a equipe técnica de um MVPD para configurar a autenticação do Adobe Primetime para atender às necessidades de quaisquer integrações existentes. A integração é gratuita para MVPDs, assumindo uma integração &quot;padrão&quot; e requisitos mínimos de suporte (documentação e suporte básico por email). Se um MVPD exigir suporte significativo ou uma linha do tempo escalada, pode ser cobrada uma taxa de suporte ou o provedor pode querer trabalhar com terceiros familiarizados com nossa solução, como o Synacor.


A autenticação da Adobe Primetime também oferece suporte para a manipulação eficiente da lógica de negócios do MVPD, da seguinte maneira:

Para uma lógica de negócios que é independente e pode ser aplicada pelo MVPD quando um pedido de autorização é recebido, o Adobe fornece os dados necessários para suportar a aplicação da lógica de negócios quando o MVPD recebe um pedido de autorização. Esses dados podem incluir, entre outros, a ID de dispositivo exclusiva para o usuário que faz a solicitação e o endereço IP do dispositivo.

Para a lógica de negócios que requer a intervenção do usuário e/ou o manuseio específico pela solução Adobe, o Adobe pode manter algumas propriedades personalizadas para cada MVPD. Essas configurações/políticas específicas do MVPD incluem a ativação de fluxos de trabalho predefinidos que podem ser iniciados em pontos específicos do fluxo de trabalho de nível superior. Para obter detalhes sobre o suporte a propriedades personalizadas, entre em contato com o representante do Adobe.

O diagrama a seguir ilustra o relacionamento do MVPD e do Programador com esses componentes de autenticação do Adobe Primetime:

![](assets/high-level-architecture-nflows.png)

*Figura: Arquitetura e fluxos de alto nível*

## Componentes de autenticação do Adobe Primetime {#components}

A seguir, é apresentada uma visão geral de alguns dos principais componentes do ecossistema de autenticação da Adobe Primetime. Isso inclui:

* [O Ativador de acesso / Serviços da Web sem cliente](#ae)
* [O servidor de back-end hospedado pelo Adobe](#backend)
* [Tokens](#tokens)

### Ativador de acesso / Serviços da Web sem cliente {#ae}

O Ativador de Acesso facilita todas as interações de autenticação e autorização com o usuário e é executado localmente em seu sistema. É o Ativador de Acesso que lida com os fluxos de trabalho de direito reais com o MVPD, enquanto o Programador mantém a responsabilidade pela página da Web ou aplicativo de player de nível superior.

Os serviços da Web sem cliente são fornecidos pela autenticação da Adobe Primetime para dispositivos que não podem renderizar páginas da Web.  Para esses dispositivos, o processo de direito é iniciado e o conteúdo é exibido no dispositivo inteligente, enquanto a autenticação com um MVPD ocorre em um dispositivo compatível com a Web (PC, smartphone e tablet).

O ativador de acesso:

* Inicia fluxos de trabalho de autenticação e autorização específicos do MVPD.
* Armazena em cache as respostas de autorização bem-sucedidas por recurso/canal do Programador para minimizar o tráfego de solicitação desnecessário.
* Pode ser configurado para workflows predefinidos específicos de cada MVPD, como registro explícito de dispositivo.
* Ele está disponível nos seguintes formulários:
   * Um arquivo SWF que o tempo de execução do Flash Player pode executar
   * Um arquivo JS executado diretamente pelo navegador
   * Um ativador de acesso nativo para várias plataformas, incluindo iOS, Android e Xbox.

### Servidor de back-end Adobe {#backend}

O servidor de back-end de autenticação da Adobe Primetime, hospedado pelo Adobe:

* Fornece os workflows de autenticação e autorização com os MVPDs que exigem comunicação servidor a servidor entre a autenticação da Adobe Primetime e o operador.
* Mantém a configuração para sites e aplicativos do Programador.
* Hospeda os arquivos de componentes do Ativador de acesso baixáveis.
* Gera tokens de autenticação e autorização.

### Tokens {#tokens}

A solução de direito de autenticação da Adobe Primetime se concentra na geração de partes específicas de dados obtidas após a conclusão com êxito dos workflows de autenticação/autorização. Esses dados são chamados de tokens. Eles têm uma vida útil limitada e são armazenados com segurança em locais dependentes da plataforma. Após a expiração, os tokens devem ser emitidos novamente por meio do reinício dos fluxos de trabalho de autenticação e/ou autorização.

Há três tipos de tokens emitidos durante os fluxos de trabalho de autenticação/autorização. Dois são &quot;de longa duração&quot;, proporcionando continuidade na experiência de visualização do usuário. O terceiro, um token de curta duração, fornece suporte para as práticas recomendadas do setor para mitigar a fraude por meio de ripagem de fluxo. Os valores de tempo de vida (&quot;TTL&quot;) para tokens são definidos com base em acordos entre MVPDs e Programadores. Você decide sobre um valor TTL que atende melhor a sua empresa e seus clientes.

**O token de autenticação de longa duração**. O sucesso da autenticação ocorre quando um cliente usa a autenticação da Adobe Primetime para fazer logon com êxito em sua conta MVPD. A autenticação da Adobe Primetime produz um token de autenticação de longa duração (&quot;authN&quot;) vinculado ao dispositivo solicitante e (dependendo do MVPD) um identificador globalmente exclusivo (&quot;GUID&quot;) que identifica o usuário anonimamente.

**O token de autorização de longa duração**. Após uma autorização bem-sucedida, a autenticação da Adobe Primetime cria um token de autorização de longa duração (&quot;authZ&quot;). Esse token não é portátil, pois está vinculado ao dispositivo solicitante e a um recurso protegido específico (por exemplo, um canal, uma série ou um episódio). O Criador de acesso usa o token authZ de longa duração para criar os tokens de mídia de curta duração usados para acessar o acesso real à visualização.

**O token de mídia de curta duração**. Depois que o usuário é autorizado, a autenticação da Adobe Primetime gera um token authZ e usa esse token para gerar um token de mídia de uso único e de curta duração que é assinado pelo Adobe e criptografado para evitar adulterações durante a troca. Como o token de curta duração é exposto ao site de incorporação por meio da API do Ativador de Acesso ou serviços da Web sem Cliente, antes de fornecer acesso ao recurso protegido, o servidor de mídia do Programador deve usar um componente de autenticação do Adobe Primetime, o Verificador de Token de Mídia, para validar o token.

## Ciclo de vida da integração MVPD {#lifecycle}

A ilustração a seguir mostra o ciclo de vida da integração entre a autenticação da Adobe Primetime e um MVPD.

![](assets/mvpd-int-lifecycle.png)

*Figura: Ciclo de vida da integração MVPD*

## Fluxograma de direitos {#chart}

O fluxograma a seguir apresenta o processo geral de confirmação do direito usando a autenticação do Adobe Primetime:

![](assets/authn-authz-entitlmnt-flow.png)

*Figura: Processo de confirmação de direito usando autenticação Adobe Primetime*

## Etapas de autenticação {#authn-steps}

As etapas a seguir apresentam um exemplo do fluxo de autenticação da Adobe Primetime.  Essa é a parte do processo de direito no qual um Programador determina se o usuário é um cliente válido de um MVPD.  Nesse cenário, o usuário é um assinante válido de um MVPD.  O usuário está tentando visualizar conteúdo protegido usando um aplicativo Flash do Programador:

1. O usuário navega até a página da Web do Programador, que carrega o aplicativo do Flash do Programador e os componentes do Ativador de acesso para autenticação da Adobe Primetime na máquina do usuário. O aplicativo Flash usa o Ativador de Acesso para definir a identificação do Programador com autenticação Adobe Primetime, e a autenticação Adobe Primetime prioriza o Ativador de Acesso com dados de configuração e estado para esse Programador (o &quot;solicitante&quot;). O Ativador de acesso deve receber esses dados do servidor antes de executar qualquer outra chamada de API.  Nota técnica: o Programador definiu sua identidade com o Enabler de Acesso `setRequestor()` método; para obter detalhes, consulte o [Guia de integração do programador](/help/authentication/programmer-integration-guide-overview.md).
1. Quando o usuário tenta visualizar o conteúdo protegido do Programador, o aplicativo do Programador apresenta ao usuário uma lista de MVPDs, a partir da qual o usuário seleciona um provedor.
1. O usuário é redirecionado para um servidor de autenticação da Adobe Primetime, onde uma solicitação SAML criptografada para o MVPD selecionado pelo usuário é criada. Esta solicitação é enviada como uma solicitação de autenticação em nome do Programador para o MVPD. Dependendo do sistema do MVPD, o navegador do usuário é redirecionado para o site do MVPD para fazer logon ou um iFrame de login é criado no aplicativo do Programador.
1. Em ambos os casos (redirecionamento ou iFrame), o MVPD aceita a solicitação e exibe sua página de logon.
1. O usuário faz logon com o MVPD, o MVPD valida o status do usuário como um cliente pagador e, em seguida, o MVPD cria sua própria sessão HTTP.
1. Quando o usuário é validado, o MVPD cria uma resposta (SAML &amp; criptografada), que o MVPD envia de volta para a autenticação da Adobe Primetime.
1. A autenticação da Adobe Primetime recebe a resposta MVPD, vê que há uma sessão HTTP de autenticação da Adobe Primetime aberta, valida o [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) resposta do MVPD e redireciona para o site do programador.
1. O site do Programador é recarregado, o Ativador de Acesso é recarregado e o Programador chama setRequestor() novamente.  A segunda chamada para setRequestor() é necessária porque a configuração atual foi alterada - agora há um sinalizador presente que informa ao Ativador de Acesso que um token AuthN está aguardando ser gerado no servidor.
1. O Ativador de Acesso vê que há uma autenticação pendente e solicita o token do servidor de autenticação da Adobe Primetime. O token é recuperado do servidor, chamando os recursos de DRM do Flash Player.
1. O token AuthN é armazenado no cache LSO do Flash Player do programador; a autenticação agora é concluída e a sessão é destruída no servidor de autenticação da Adobe Primetime.

## Etapas de autorização {#authz-steps}

As etapas a seguir continuam a partir da seção anterior ([Etapas de autenticação](#authn-steps)):

1. Quando o usuário tenta acessar o conteúdo protegido do Programador, o aplicativo do Programador verifica primeiro se há um token AuthN no computador ou dispositivo local do usuário.  Se esse token não estiver lá, então a variável [Etapas de autenticação](#authn-steps) acima são seguidas.  Se o token AuthN estiver lá, o fluxo de Autorização continuará com o aplicativo do Programador iniciando uma chamada para o Criador de Acesso com uma solicitação para obter os direitos de visualização do usuário para um item específico de conteúdo protegido.
1. O item específico de conteúdo protegido é representado por um &quot;identificador de recurso&quot;.  Pode ser uma sequência simples ou uma estrutura mais complexa, mas em qualquer caso a natureza do identificador de recursos é acordada antecipadamente entre o programador e o MVPD.  O aplicativo do Programador passa o identificador de recurso para o Ativador de Acesso.  O Ativador de Acesso verifica se há um token AuthZ no computador ou dispositivo local do usuário.  Se o token AuthZ não estiver lá, o Habilitador de acesso passará a solicitação para o servidor de autenticação da Adobe Primetime de back-end.
1. O servidor de autenticação da Adobe Primetime se comunica com o endpoint de autorização MVPDs usando protocolos padronizados.  Se a resposta do MVPD indicar que o usuário tem direito a exibir o conteúdo protegido, o servidor de autenticação da Adobe Primetime cria um token AuthZ e o transmite para o Ativador de acesso, que armazena o token AuthZ na máquina do usuário.
1. Com um token AuthZ armazenado no computador ou no dispositivo do usuário, o aplicativo Programador chama o Criador de acesso para obter um Token de mídia do servidor de autenticação da Adobe Primetime e fornece esse token para o aplicativo do Programador.
1. Por fim, o aplicativo do Programador usa o componente Verificador de token de mídia para confirmar que o usuário correto está visualizando o conteúdo correto, e com o Token de mídia no lugar, o usuário tem permissão para visualizar o conteúdo protegido.

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Primetime authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
