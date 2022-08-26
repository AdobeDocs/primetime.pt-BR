---
title: Visão geral da REST API
description: Visão geral das Rest APIs
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Visão geral da REST API {#rest-api-overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Visão geral {#over}

A API REST de autenticação da Adobe Primetime fornece acesso direto aos serviços de autenticação e autorização da TV em qualquer lugar (TVE). Essa API suporta duas arquiteturas principais: Dispositivos de servidor para servidor ou conectados (por exemplo, consoles de jogos, TVs inteligentes, conversores, etc.) aplicativos que não possuem recursos de navegação na Web. 

 

### Servidor para servidor

As soluções de servidor para servidor envolvem aplicativos cliente do Programador que se integram a serviços do Programador que se conectam com os serviços de autenticação da Adobe Primetime para fluxos TVE. Essa abordagem transfere a maior parte da implementação de TVE do cliente para o servidor, onde um único módulo de autorização unificado pode ser criado e mantido. A principal responsabilidade restante dos aplicativos clientes é o gerenciamento de uma visualização da Web para autenticação de usuário.

 

### Dispositivos conectados

Os aplicativos Dispositivos conectados se comunicam diretamente com a Autenticação do Primetime por meio das APIs REST para executar a configuração, o registro, as verificações de status de autenticação e os fluxos de autorização, enquanto um segundo aplicativo de tela (navegador) é necessário para o fluxo de autenticação. Dessa forma, os SDKs nativos não são usados.

 

### Outras arquiteturas

Além das duas principais arquiteturas baseadas na REST API, as soluções de cliente Servidor para servidor e Direto para dispositivos inteligentes, há outras arquiteturas.  Dentre elas, está a arquitetura do SDK, que usa um componente cliente chamado Ativador de acesso que a autenticação do Primetime fornece aos programadores.  O aplicativo usa APIs do ativador de acesso para lidar com inicialização, autenticação, autorização e logout.  Toda a comunicação entre o aplicativo do Programador e os servidores de autenticação do Primetime ocorre por meio do Ativador de Acesso.  Um modo diferente de Ativador de acesso está disponível para as seguintes plataformas: JavaScript, iOS, tvOS, Android e FireTV.

Embora seja possível usar a REST API diretamente em plataformas de clientes que suportam SDKs nativos fora de uma solução servidor para servidor, essa abordagem não é recomendada.

 

## Vantagens e desvantagens da API REST {#ProsAndCons}

A API REST de autenticação do Adobe Primetime foi criada para fornecer uma solução de TV em qualquer lugar (TVE) para dispositivos que não têm recursos de navegação na Web ou armazenamento persistente. A REST API fornece suporte para todos os fluxos de autenticação e autorização, mas porque ela não tem um componente SDK nativo. Os SDKs fornecidos e mantidos pela Autenticação Adobe Primetime vêm com funcionalidades prontas para uso que implementam regras de negócios que, no caso da API REST, devem ser implementadas e mantidas pelos Programadores. Na tabela Responsabilidades do programador abaixo descrevemos as limitações da REST API atual que precisam ser abordadas pelos programadores.

 

### Vantagens e desvantagens baseadas em cliente e de servidor para servidor

Uma arquitetura servidor para servidor fornece uma maneira de consolidar a maior parte da lógica relacionada à autenticação e autorização em uma única unidade lógica ou implementação.  Essa abordagem tem vantagens e desvantagens.  As vantagens incluem:

* Implementação única para a lógica comercial de autenticação e autorização.
* Evite a necessidade de implementar essa lógica em cada plataforma compatível usando as ferramentas nativas dessas plataformas.
* A capacidade de atualizar recursos sem precisar atualizar clientes com todos os requisitos associados (por exemplo, atualizações da loja de aplicativos).
* **Mais facilmente** estender e personalizar os recursos authN e authZ (por exemplo, adicionar D2C).
* Gestão direta do tráfego associado para um maior controlo, qualidade e monitorização.

 

Novamente, os ícones são listados nas responsabilidades do Programador, mas incluem o seguinte:

* O SSO deve ser implementado para cada cliente para plataformas sem o SSO da plataforma.
* Se necessário, os programadores devem implementar uma lógica específica para MVPD.
* Todas as plataformas que usam a REST API compartilham uma única configuração que rege propriedades, como TTLs de autenticação.

 

### Dispositivos conectados

Para a maioria dos dispositivos conectados, a API REST deve ser usada de uma maneira ou de outra, pois um SDK não está disponível. O dispositivo conectado usará a REST API diretamente ou se integrará a uma solução de servidor para servidor que usa a REST API.

## Responsabilidades do programador {#programmer-responsibilities}

O seguinte se aplica aos aplicativos Servidor para Servidor e Dispositivo Conectado.

| **Funcionalidade** | **Responsável pela gestão da funcionalidade** | **Descrição das limitações da API sem cliente atual e diferenças em relação aos SDKs nativos** |
| --- | --- | --- |
| Configurações aplicadas por Plataforma | Adobe | One **limitação importante** ao usar a REST API em todas as plataformas (incluindo dispositivos móveis como iOS e Android), as configurações correspondentes à REST API na ferramenta de configuração do TVE Dashboard são aplicadas em todos os dispositivos (mesmo se houver um dispositivo iOS que executa um aplicativo nativo implementado sobre a REST API). Esta limitação **pode quebrar** os TTLs acordados e as configurações de plataforma acordadas com os MVPDs - se forem diferentes para cada plataforma. [1](#1) |
| Logon único | Programadores | Usando a REST API, o SSO só está disponível nas plataformas que oferecem suporte ao SSO da plataforma (por exemplo, Apple, Roku, Amazon), enquanto o SSO não pode ser garantido para outras plataformas ao usar a REST API. Os SDKs armazenam dados em cache de forma entre sites/aplicativos. Isso significa que o usuário faz logon uma vez em um site/aplicativo e já está conectado em sites participantes, sem nenhuma interação do usuário necessária. [2](#2) |
| Logout único | Programadores | Em um cenário nativo de SDK SSO, encerrar a sessão de um aplicativo participante encerra a sessão do usuário de todos os locais. Na API REST atual, não oferecemos suporte ao SLO, encerrar a sessão a partir de um aplicativo encerra a sessão do utilizador apenas para esse aplicativo específico. |
| Armazenamento em cache | Programadores | As implementações da REST API terão que implementar seu próprio mecanismo de armazenamento em cache para itens de dados acordados pelos negócios. Os SDKs armazenam automaticamente em cache vários itens de dados, ao mesmo tempo em que consideram várias regras de negócios. Por exemplo, os metadados do usuário são armazenados em cache com o mesmo TTL do token de autenticação, enquanto alguns itens podem ser programaticamente excluídos do armazenamento em cache (comprovação). |
| Mecanismo detalhado de relatório de erros | Programadores | A REST API depende principalmente de códigos de erro HTTP para relatar erros do aplicativo, enquanto os SDKs têm um mecanismo detalhado de relatório de erros que ajuda os desenvolvedores do aplicativo a entender melhor o que está acontecendo. |
| Recuperação de erros do aplicativo (tentativa de erro, detecção de loop etc.) | Programadores | As implementações da REST API precisam criar seus próprios sistemas de recuperação de aplicativos, enquanto as implementações sobre SDKs se beneficiam do sistema de recuperação de erros dos SDKs: recuperação de erros de rede transitórios, tentando novamente determinadas chamadas de rede com lógica em vigor para evitar &quot;loops&quot;. |
| Autenticação por solicitante | Programadores | Alguns MVPDs exigem autenticação para cada site/aplicativo, por motivos comerciais ou devido a desafios técnicos. Os SDKs impõem automaticamente isso com base na configuração do painel TVE. Os implementadores da API REST devem implementá-la eles mesmos, a fim de não violar os acordos comerciais, ou para poder concluir a autorização para os MVPDs que têm o escopo de seus dados de autenticação por aplicativo. |
| Autenticação passiva | Programadores | Alguns MVPDs são compatíveis com autenticação &quot;passiva&quot;, onde o usuário não é obrigado a inserir as credenciais, e uma tentativa de autenticação do usuário é feita automaticamente. Isso é especialmente útil para MVPDs que também têm &quot;Autenticação por solicitante&quot; como um requisito. Nesse caso, o UX ativado pelos SDKs é perfeito, onde o usuário é autenticado apenas uma vez em um aplicativo e o SDK realiza autenticação &quot;passiva&quot; para outros aplicativos no ecossistema. O usuário não vê as chamadas passivas adicionais, ele simplesmente já estará autenticado, enquanto o MVPD atinge o objetivo de ter sessões de autenticação separadas para cada aplicativo. |
| Detecção de dispositivos implícita e uniforme | Programadores | Os SDKs detectam automaticamente o tipo de dispositivo e enviam essas informações de uma maneira padrão. As implementações da API REST podem enviar informações diferentes, dependendo do implementador, distorcendo/quebrando regras e estatísticas de negócios entre sites. **Os programadores precisam verificar se nos enviaram corretamente [informações do dispositivo](http://tve.helpdocsonline.com/passing-device-information) em cada uma das** aplicativos. Para implementações de servidor para servidor, a api REST não identifica corretamente o endereço IP do usuário final, a menos que sejam tomadas etapas adicionais. O endereço IP é importante em certos casos de uso, como prevenção de fraude ou HBA. Consulte [como passar o endereço IP do cliente em implementações do lado do servidor](http://tve.helpdocsonline.com/clientless-integration-cookbook-v2$overall_clientIP). |
| TempPass à prova de adulteração | Programadores | A imposição do TempPass é baseada em uma ID de dispositivo estável. Os SDKs usam técnicas de informações/impressões digitais de hardware para identificar o dispositivo e esse mecanismo não é público, portanto, é mais seguro e sem colisões. Para implementações de REST API, os Programadores precisam implementar seus próprios algoritmos para identificação/impressão digital de dispositivo. |
| Ligação de dispositivo | Programadores | Tokens gerados em um dispositivo com um aplicativo por SDK não são portáteis, tornando difícil para um usuário mal-intencionado compartilhar seus tokens e fornecer acesso a outros usuários. Isso se baseia no mesmo mecanismo de ID do dispositivo que o &quot;TempPass de prova de violação&quot;. Para a API REST, os tokens permanecem na nuvem, o que significa que dois dispositivos com as mesmas deviceIDs fazendo as mesmas chamadas receberão as mesmas respostas/acesso. Os programadores precisam ter certeza de que têm um mecanismo robusto, seguro e sem colisões para gerar/alocar deviceIDs. |
| Previsível e conjunto certificado de recursos | Programadores | O conjunto existente de recursos em cada SDK é consistente, previsível e totalmente certificado e testado. Alguns requisitos de negócios são aplicados por meio dos SDKs, o que torna arriscado para o programador quebrar contratos ao usar a REST API. Embora a REST API possa ser mais flexível, o Adobe garante que as implementações do SDK apliquem as decisões de negócios e as configurações do TVE Dashboard. No caso de Clientless, cada Programador implementa seu próprio subconjunto de regras de negócios que suíte seus aplicativos em um determinado ponto no tempo. |


1. Como parte da nova iniciativa Uma API, pretendemos corrigir essa limitação e poder aplicar regras por plataforma com base na identificação do dispositivo.

2. O Adobe continua a funcionar com todas as principais plataformas para implementar o SSO da plataforma que pode ser usado com nossa REST API. Nossa iniciativa de Uma API oferecerá suporte de SSO entre aplicativos implementados com SDKs e aplicativos nativos implementados com a API REST.

## Requisitos mínimos do dispositivo {#min_reqs}

Para usar a API REST de autenticação do Primetime, os dispositivos devem atender ou exceder os requisitos técnicos mínimos listados na seção REST API do [Documento de requisitos de plataforma / dispositivo / ferramentas de autenticação do Primetime](#general_clientless_reqs).

## Recursos relacionados {#related}

* [Fluxo de direitos do programador](https://tve.helpdocsonline.com/entitlement-flow)
* [Referência da API REST](http://tve.helpdocsonline.com/registration-code-request)
* [Livro da API REST (servidor para servidor)](http://tve.helpdocsonline.com/rest-api-cookbook-server-to-server) 
* [Guia da API REST (cliente para servidor)](http://tve.helpdocsonline.com/rest-api-cookbook-client-to-server)

<!--* [Platform / Device / Tool Requirements](#)-->
