---
title: Casos de uso do programador
description: Casos de uso do programador
exl-id: 51ca7e4f-b0d8-4e35-8398-2efb4879de2a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 0%

---

# Casos de uso do programador {#programmer-use-cases}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Visão geral {#overview}

Este documento resume os casos de uso da integração do programador compatíveis com a autenticação da Adobe Primetime. Verifique esta página antes de iniciar um projeto de integração para ver quais recursos são compatíveis no momento.

## Casos de uso {#use-cases}


### Integração básica: autenticação e autorização federadas para uma única rede de canal {#basic-integration}

**Prioridade** - Alta

**Detalhamento** - aplicativo TVE com marca de programador único com 1 Channel Network hospedado dentro da experiência

Isso permite que os programadores ofereçam conteúdo premium, em seu próprio aplicativo TVE* de marca, com uma verificação de direito federado para o MVPD. A requestorID deve ser alinhada para corresponder à marca do aplicativo que veicula o conteúdo para o visualizador. Nesse cenário, há uma relação de 1 para 1 entre a ID do solicitante de autenticação da Adobe Primetime e a ID do recurso que é verificada em relação aos direitos.

>[!NOTE]
>
>O aplicativo TVE é usado neste documento para fazer referência coletiva aos diferentes tipos de aplicativos (aplicativos web, aplicativos móveis etc.) suportado pela autenticação Adobe Primetime. A coluna Plataformas abaixo pode conter detalhes sobre as plataformas compatíveis para casos de uso específicos.

#### Casos de uso específicos (comuns à maioria das integrações) {#sp-use-cases-basic-int}

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|:--------:|:-----------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------:|:-----------------------------------------:|
| Alta | Descoberta MVPD do Aplicativo TVE do Programador | O usuário inicia no aplicativo TVE com marca do Programador e é solicitado a selecionar seu Provedor de MVPD. | API sem cliente da Web (SWF/JS) Mobile (iOS/Android) (para 2ª tela) |  |
| Alta | Autenticação federada do aplicativo TVE do programador | O usuário inicia no aplicativo TVE com marca do Programador e, após selecionar o Provedor MVPD, o usuário é transferido para a página de logon do próprio MVPD para inserir suas credenciais. | Web (SWF/JS) Mobile (iOS/Android) |  |
| Alta | Autorização do aplicativo TVE do programador | Depois que o usuário é autenticado, o aplicativo TVE do programador pode fazer solicitações de autorização de canal de retorno para o MVPD para verificar os direitos do usuário. Normalmente, isso é apenas verificar se a Rede de canal está no pacote de assinatura MVPD dos usuários.                                  Nesse caso, a ID do solicitante e a ID do recurso corresponderão 1:1. | Todas as plataformas |  |
| Medium | Fazer logoff do aplicativo TVE do programador | Permite que o usuário faça logout e limpe os tokens AuthN/AuthZ de autenticação da Adobe Primetime. Em muitos casos, isso também desconecta o usuário do MVPD. Mas os MVPDs variam se isso for suportado. Ela sempre limpa a sessão de autenticação e os tokens do Adobe Primetime. | Todas as plataformas, exceto XBox nativo | Vários MVPDs não oferecem suporte a isso. |
| Alta | Logon único em sites e aplicativos | Permite que o usuário compartilhe a sessão de logon em sites e aplicativos sem a necessidade de fazer logon novamente. | Todas as plataformas, exceto a API sem cliente | Exige pelo menos SDK 1.7 para alguns MVPDs. |

### Aplicativo TVE único que hospeda várias redes de canal {#single-app-multi-channel}

**Prioridade**- Alta

Permite que o programador agregue várias redes de canal de conteúdo no mesmo destino de marca para seus visualizadores.

#### Casos de uso específicos {#sp-use-cases-singl-tve-app}

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Alta | Autorização de canal distinto | O usuário pode assistir ao conteúdo de várias redes de canal dentro do mesmo aplicativo TVE. O Programador é capaz de fazer chamadas de autorização específicas para cada rede de canal para confirmar os direitos dos usuários. | Todas as plataformas | Todos os MVPDs agora oferecem suporte a isso de alguma forma. |
| Baixa | Consulta de autorização de comprovação | Isso permite que o programador verifique quais canais o usuário tem em seu pacote em uma única chamada de API. Isso é feito antes das chamadas de AuthZ reais para filtrar o conteúdo da interface à qual o usuário não tem acesso. |  | A maioria dos MVPDs ainda não expõe esses dados como Atributos do usuário, portanto, o Adobe realmente faz chamadas de AuthZ para obtê-los. Além disso, a maioria dos MVPDs é limitada a 5 por vez, pois não são compatíveis com vários canais em uma única chamada.                             É muito importante verificar quantos canais o programador precisa verificar. Independentemente do número, teremos que verificar se está correto com os MVPDs. Atualmente, a maioria dos MVPDs não é compatível (3º trimestre de 2013) com mais de 5 canais. |

### Autorização no nível do ativo {#asset-level-authz}

**Prioridade** - Baixa

**Detalhamento** - Transmitir Um Identificador De Ativo Na Solicitação De Autorização

**Plataformas** - Todas as plataformas

#### Casos de uso específicos {#sp-use-cases-asset-lvl-authz}

Habilita o MVPD para obter análise no nível do ativo em cada chamada AuthZ. Isso tem a desvantagem de negar o cache AuthZ de autenticação do Adobe Primetime.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------------|--------------------------------------|
| Baixa | Transmitir um identificador de ativo na solicitação de autorização | Habilita o MVPD para obter análise no nível do ativo em cada chamada AuthZ.  Tem a desvantagem de negar o cache AuthZ de autenticação do Adobe Primetime. | Todas as plataformas | Apenas um MVPD oferece suporte a isso no momento. |




### Controles dos pais {#parental-controls}

**Prioridade** - Baixa

Permite que restrições de conta de usuário do MVPD sejam aplicadas ao aplicativo TVE do programador.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|-----------------------------------|
| Baixa | Filtrar conteúdo com base nos atributos do usuário | Permite que o programador verifique a Classificação máxima permitida para um usuário antes de renderizar a lista de conteúdo disponível para o usuário. | Web (Flash/JS) Mobile (iOS/Android) | Atualmente, só funciona com um MVPD. |
| Baixa | Transmita classificações de conteúdo na solicitação AuthZ | Permite que o Programador transmita a classificação específica do conteúdo que o usuário deseja assistir como parte da solicitação AuthZ para o MVPD Relacionado a #3, já que as classificações normalmente estão no nível do ativo. | Todas as plataformas | Atualmente, só funciona com um MVPD. |

#### Personalização da integração MVPD por marca de programador {#mvpd-int-cust-prog-brand}

**Prioridade** - Médio

Habilita a experiência personalizada durante o AuthN ou para mensagens de erro de AuthZ.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------------------------------------|
| Medium | Transmita o identificador do provedor de serviços na solicitação de autenticação. | Ative a marca específica na página de logon do MVPD específica do provedor de serviços. Habilite também a seleção automática do padrão para corresponder ao público-alvo, como espanhol para Univision. | Todas as plataformas | Varia por MVPD. Alguns não suportam isso. |
| Medium | Mensagens de Erro Personalizadas na Resposta AuthZ | Habilita mensagens de erro específicas do Programador ou da marca do MVPD que podem incluir uma mensagem específica para venda adicional com um link que atualiza o pacote. | Web, Android, iOS | Varia por MVPD. Alguns não suportam isso. |


### Casos de uso do dispositivo conectado {#connected-devices}

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medium | XBox LiveID SSO em aplicativos e consoles | Permite que o usuário compartilhe uma sessão AuthN entre aplicativos e entre diferentes consoles de jogos - vinculados à sua conta LiveID. | SDK nativo do XBox | A maioria dos MVPDs não gosta disso porque o modelo típico é vincular o token ao dispositivo, não ao usuário.                             Se for possível, não recomendamos mais essa abordagem. |
| Alta | Dispositivo conectado com tokens vinculados à appID no dispositivo | Permite que o Programador vincule o direito de MVPD no token à appID no dispositivo para o qual foi emitido. | API sem cliente | Isso alinha o Dispositivo conectado mais estreitamente à implementação padrão de Aprovação para tokens.                             O ainda precisa de melhorias para ser uma ID para todo o dispositivo. |

### Comprimento TTL de AuthN específico do dispositivo {#authn-ttl-length}

Habilite o direito de TVE para eventos especiais que podem não ser recursos do banco de dados de direitos do MVPD, como canais normais.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|--------------------------------------------------------------------------------------------------------------------------|
| Alta | Definir valores TTL diferentes por plataforma | Permite que o Programador estabeleça um comprimento TTL diferente para dispositivos da Web, móveis e conectados. Atualmente, a autenticação da Adobe Primetime é compatível com a capacidade de ter três valores TTL separados: Web (Flash) Mobile/HTML5 Clientless - Connected Devices |  | Alguns MVPDs definem o TTL dinamicamente. O Adobe pode substituir essas configurações dinâmicas, se necessário, usando as configurações. |

### Aplicativos especiais baseados em eventos {#special-event}

**Prioridade** - Baixa

Habilite o direito de TVE para eventos especiais que podem não ser recursos do banco de dados de direitos do MVPD, como canais normais.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|------------------------------------------|
| Baixa | Vários canais como um proxy para um evento | Isso foi feito para as Olimpíadas, onde o assinante precisava ter dois canais diferentes em seu pacote para ter acesso. Nesse caso, a autenticação do Adobe Primetime criou um novo resourceID e fez com que todos os MVPDs fizessem o mapeamento para os canais específicos da extremidade deles.  Funcionou bem com aviso prévio suficiente. Isso foi importante porque a maioria dos MVPDs não oferece suporte a várias chamadas de recursos. | Todas as plataformas | Suportado por todos os MVPDs com aviso prévio adequado. |
| Baixa | Novo aplicativo de evento especial, usando recursos de canal existentes | Isso foi feito para a Loucura de março. O provedor de conteúdo criou um novo aplicativo com uma nova ID de solicitante. Todos os MVPDs necessários para adicionar suporte ao novo requestorID em seus sistemas. As resourceIDs eram canais normais.  Alguns MVPDs também precisavam mapear os canais como válidos sob o novo solicitante, portanto, era necessário mais tempo para esses casos. | Todas as plataformas | Suportado por todos os MVPDs com aviso prévio adequado. |
| Baixa | RequestorID, resourceID existente | Isso foi feito para o torneio de fim de semana de golfe Masters. Foi apenas um pequeno evento por alguns dias, e os Masters tiveram seu próprio aplicativo móvel que estava bem para exibir o conteúdo. O programador planejou pagar pelo tráfego de autenticação da Adobe Primetime e usar apenas a requestID e a resourceID padrão. O único truque foi fazer com que o Programador compartilhasse um certificado móvel para a assinatura do ID do solicitante com os mestres e adicionasse isso à configuração deles como certificado de backup para esse fim de semana. | Todas as plataformas | Nenhum impacto para MVPDs |

### Integração do servidor de conteúdo {#content-server-integration}

**Prioridade**- Médio

Ativar a validação do token de mídia antes de liberar o fluxo de vídeo para o reprodutor do cliente.
| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD | |—|—|—|—|—| | Alto | Programador Federated Player - Com Autorização No Nível Da Página | As APIs de autenticação da Adobe Primetime são feitas em JavaScript na página, e o token é passado para o reprodutor. O token pode ser passado para o serviço de validação de várias maneiras: Obter o parâmetro no parâmetro de URL do serviço de validação transmitido na sequência de consulta da API de interface externa do URL de fluxo FlashVars | | | | Médio | Programador Federated Player - Com autorização interna do player | As APIs de autenticação do Adobe Primetime são feitas no ActionScript no SWF do reprodutor, portanto, o token está disponível para o reprodutor a partir do retorno de chamada.                                                                                                                                                                                         | | | | Alto | Player sindicalizado - hospedado no portal MVPD com autorização em nível de página usando um iFrame para envolver o player | Semelhante ao reprodutor com autorização em nível de página, mas com o invólucro de página do reprodutor iFramed no portal MVPD. A autenticação deve ocorrer separadamente no portal MVPD.                                                                                                                                                    |           |                        |


<!--
>[!RELATEDINFORMATION]
>
>* MVPD Integration Features
>* Entitlement Flow
>* Platform / Device Requirements
-->
