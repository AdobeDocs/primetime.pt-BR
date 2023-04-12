---
title: Casos de uso do programador
description: Casos de uso do programador
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 0%

---


# Casos de uso do programador {#programmer-use-cases}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview}

Este documento resume os casos de uso da integração do Programador compatíveis com a autenticação da Adobe Primetime. Você pode verificar essa página antes de iniciar um projeto de integração para ver quais recursos são suportados atualmente.

## Casos de uso {#use-cases}


### Integração básica: Autenticação e autorização federadas para uma rede de canal único {#basic-integration}

**Prioridade** - Alto

**Detalhamento** - Aplicativo TVE com a marca de um único programador com 1 Canal de rede hospedado na experiência

Isso permite que os programadores ofereçam conteúdo premium, em seu próprio aplicativo TVE de marca*, com uma verificação de direito federada para o MVPD. A requestorID deve ser alinhada para corresponder à marca do aplicativo que veicula o conteúdo para o visualizador. Nesse cenário, há uma relação de 1 a 1 entre a ID do Solicitante de autenticação da Adobe Primetime e a ID do recurso que é verificada para o direito.

>[!NOTE]
>
>O aplicativo TVE é usado neste documento para se referir coletivamente aos diferentes tipos de aplicativos (aplicativos da Web, aplicativos móveis etc.) suportado pela autenticação da Adobe Primetime. A coluna Plataformas abaixo pode conter detalhes sobre plataformas compatíveis para casos de uso específicos.

#### Casos de uso específicos (comuns à maioria das integrações) {#sp-use-cases-basic-int}

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|:--------:|:-----------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------:|:-----------------------------------------:|
| Alto | Descoberta MVPD do Aplicativo TVE do Programador | O usuário inicia no aplicativo TVE da marca do Programador e é solicitado a selecionar seu Provedor MVPD. | API sem cliente Web (SWF/JS) móvel (iOS/Android) (para segunda tela) |  |
| Alto | Autenticação Federada do Aplicativo TVE do Programador | O usuário inicia no aplicativo TVE com a marca do Programador e, depois de selecionar o Provedor MVPD, o usuário é transferido para a página de logon do MVPD para inserir suas credenciais. | Web (SWF/JS) Móvel (iOS/Android) |  |
| Alto | Autorização do aplicativo TVE do programador | Depois que o usuário é autenticado, o aplicativo TVE do Programador pode fazer solicitações de autorização de canal traseiro ao MVPD para verificar o direito do usuário. Geralmente, isso é apenas verificar se a Rede de canal está no pacote de assinatura MVPD dos usuários.                                  Nesse caso, a ID do solicitante e a ID do recurso corresponderão 1:1. | Todas as plataformas |  |
| Médio | Logout do aplicativo TVE do programador | Permite que o usuário desconecte e limpe os tokens AuthN/AuthZ de autenticação da Adobe Primetime. Em muitos casos, isso também faz logoff do usuário do MVPD. Mas os MVPDs variam se isso é suportado. Ele sempre limpa a sessão de autenticação do Adobe Primetime e os tokens. | Todas as plataformas, exceto XBox Nativo | Vários MVPDs não suportam isso. |
| Alto | Logon único em Sites e Aplicativos | Permite que o usuário compartilhe a sessão de logon entre sites e aplicativos sem precisar fazer logon novamente. | Todas as plataformas, exceto API sem cliente | Exige pelo menos o SDK 1.7 para alguns MVPDs. |

### Aplicativo TVE único que hospeda várias redes de canal {#single-app-multi-channel}

**Prioridade**- Alto

Permite que o Programador agregue várias redes de canais de conteúdo no mesmo destino de marca para seus visualizadores.

#### Casos de uso específicos {#sp-use-cases-singl-tve-app}

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Alto | Autorização de canal distinta | O usuário pode assistir ao conteúdo de várias redes de canais dentro do mesmo aplicativo TVE. O Programador pode fazer chamadas de autorização específicas para cada rede de canal para confirmar o direito dos usuários. | Todas as plataformas | Todos os MVPDs agora suportam isso de alguma forma. |
| Baixo | Consulta de Autorização de Comprovação | Isso permite que o Programador verifique quais canais o usuário tem em seu pacote em uma única chamada de API. Isso é feito antes das chamadas AuthZ reais para filtrar o conteúdo da interface de usuário que o usuário não tem acesso. |  | A maioria dos MVPDs ainda não expõe esses dados como Atributos do usuário, então o Adobe faz chamadas de AuthZ para obtê-los. Além disso, a maioria dos MVPDs é limitada a 5 de cada vez, pois não suporta vários canais em uma única chamada.                             É muito importante verificar quantos canais o Programador precisa verificar previamente. Não importa qual seja o número, vamos precisar verificar se está tudo bem com os MVPDs. No momento, a maioria dos MVPDs não é compatível com mais de cinco canais (terceiro trimestre de 2013). |

### Autorização a nível de ativos {#asset-level-authz}

**Prioridade** - Baixo

**Detalhamento** - Enviar Um Identificador De Ativo Na Solicitação De Autorização

**Plataformas** - Todas as plataformas

#### Casos de uso específicos {#sp-use-cases-asset-lvl-authz}

Permite que o MVPD obtenha análises de nível de ativo em cada chamada de AuthZ. Isso tem a desvantagem de negar o cache AuthZ de autenticação da Adobe Primetime.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------------|--------------------------------------|
| Baixo | Enviar um identificador de ativo na solicitação de autorização | Permite que o MVPD obtenha análises de nível de ativo em cada chamada de AuthZ.  Tem o lado negativo de negar o cache AuthZ de autenticação da Adobe Primetime. | Todas as plataformas | Somente um MVPD suporta isso atualmente. |




### Controles dos pais {#parental-controls}

**Prioridade** - Baixo

Permite que restrições da conta de usuário do MVPD sejam aplicadas no aplicativo TVE do Programador.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|-----------------------------------|
| Baixo | Filtrar conteúdo com base em atributos do usuário | Permite que o Programador verifique a Classificação máxima permitida para um usuário antes de renderizar a lista de conteúdo disponível para o usuário. | Web (Flash/JS) Móvel (iOS/Android) | Funciona somente com um MVPD no momento. |
| Baixo | Envio de classificações de conteúdo na solicitação AuthZ | Permite que o Programador passe a classificação específica do conteúdo que o usuário deseja assistir como parte da solicitação AuthZ para o MVPD Relacionado ao #3, já que as classificações normalmente estão no nível do ativo. | Todas as plataformas | Funciona somente com um MVPD no momento. |

#### Personalização da integração do MVPD por marca de programador {#mvpd-int-cust-prog-brand}

**Prioridade** - Médio

Habilita a experiência personalizada durante AuthN ou para mensagens de erro de AuthZ.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------------------------------------|
| Médio | Envio do Identificador do Provedor de Serviços na Solicitação AuthN. | Ative a marca específica na página de logon do MVPD específica do provedor de serviços. Além disso, ative a seleção automática do padrão para corresponder ao público-alvo, como Espanhol para visão. | Todas as plataformas | Varia de MVPD. Há quem não apoie esta posição. |
| Médio | Mensagens de erro personalizadas na resposta de AuthZ | Habilita mensagens de erro específicas do programador ou da marca do MVPD que podem incluir mensagens específicas de venda adicional com um link que atualize o pacote. | Web, Android, iOS | Varia de MVPD. Há quem não apoie esta posição. |


### Casos de uso do dispositivo conectado {#connected-devices}

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Médio | XBox LiveID SSO em aplicativos e consoles | Permite que o usuário compartilhe a sessão AuthN entre aplicativos e entre diferentes consoles de jogos - vinculados à conta LiveID. | SDK nativo do XBox | A maioria dos MVPDs não gosta disso porque o modelo típico é vincular o token ao dispositivo - não ao usuário.                             Não recomendamos mais essa abordagem se for possível. |
| Alto | Dispositivo conectado com tokens vinculados à appID no dispositivo | Permite que o Programador vincule o direito do MVPD no token ao appID no dispositivo para o qual foi emitido. | API sem cliente | Isso alinha o Dispositivo conectado mais à implementação padrão de Pass para tokens.                             Ainda precisa de melhorias para ser uma ID de todo o dispositivo. |

### Comprimento do TTL AuthN específico do dispositivo {#authn-ttl-length}

Habilite o direito TVE para eventos especiais que podem não ser recursos que estão no banco de dados de direito MVPD como canais normais.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|--------------------------------------------------------------------------------------------------------------------------|
| Alto | Definir diferentes valores de TTL por plataforma | Permite que o Programador estabeleça um tamanho TTL diferente para dispositivos Web, móveis e conectados. Atualmente, a autenticação da Adobe Primetime suporta a capacidade de ter 3 valores TTL separados: Web (Flash) móvel/HTML5 sem cliente - Dispositivos conectados |  | Alguns MVPDs definem o TTL dinamicamente. O Adobe pode substituir essas configurações dinâmicas, se necessário, usando as configurações. |

### Aplicativos especiais baseados em eventos {#special-event}

**Prioridade** - Baixo

Habilite o direito TVE para eventos especiais que podem não ser recursos que estão no banco de dados de direito MVPD como canais normais.

| Prioridade | Caso de uso | Descrição | Plataformas | Notas do MVPD |
|--------|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|------------------------------------------|
| Baixo | Vários canais como proxy para um evento | Isso foi feito para as Olimpíadas, onde o assinante precisava ter dois canais diferentes em seu pacote para ter acesso. Nesse caso, a autenticação da Adobe Primetime criou uma nova resourceID e fez com que todos os MVPDs fizessem o mapeamento para os canais específicos em seu lado.  Isso funcionou bem com um aviso prévio suficiente. Isso foi importante porque a maioria dos MVPDs não suporta várias chamadas de recurso. | Todas as plataformas | Suportado por todos os MVPDs com aviso adequado. |
| Baixo | Novo Aplicativo de Evento Especial, Usando Recursos de Canal Existentes | Isso foi feito pela Marcha Madness. O provedor de conteúdo criou um novo aplicativo com uma nova ID do solicitante. Todos os MVPDs necessários para adicionar suporte para o novo requestorID em seu sistema. As resourceIDs eram canais normais.  Alguns MVPDs também precisavam mapear os canais como válidos sob o novo solicitante, então era necessário mais tempo para esses casos. | Todas as plataformas | Suportado por todos os MVPDs com aviso adequado. |
| Baixo | ID do solicitante existente, resourceID | Isso foi feito para o torneio de fim de semana de golfe dos Masters. Foi apenas um pequeno evento por alguns dias, e os Mestres tiveram seu próprio aplicativo móvel que estava certo para exibir o conteúdo. O Programador planejou pagar pelo tráfego de autenticação do Adobe Primetime e usar apenas a ID de solicitação e a ID de recurso padrão. O único truque era fazer com que o Programador compartilhasse um certificado móvel para assinatura requestorID com os Mestres e adicionasse isso à configuração como certificado de backup para aquele fim de semana. | Todas as plataformas | Nenhum impacto para MVPDs |

### Integração do servidor de conteúdo {#content-server-integration}

**Prioridade**- Médio

Ativar a validação do token de mídia antes de lançar o fluxo de vídeo no reprodutor do cliente.
| Prioridade | Caso de uso | Descrição | Plataformas | Notas MVPD | |—|—|—|—|— | Alto | Reprodutor federado do programador - Com autorização no nível da página | As APIs de autenticação da Adobe Primetime são feitas em JavaScript na página e o token é passado para o player. O token pode ser transmitido ao serviço de validação de algumas maneiras: Obter parâmetro no parâmetro do URL do serviço de validação passado na string de consulta do URL de fluxo API FlashVars da interface externa | | | | Médio | Reprodutor Federado Do Programador - Com Autorização Interna Do Reprodutor | As APIs de autenticação do Adobe Primetime são feitas no ActionScript no SWF do reprodutor, portanto, o token está disponível para o reprodutor a partir do retorno de chamada.                                                                                                                                                                                         | | | | Alto | Player sindicalizado - hospedado no portal MVPD com autorização no nível da página usando um iFrame para colocar o reprodutor em contorno | Semelhante ao reprodutor com autorização no nível da página, mas com o iFrame do wrapper de páginas do reprodutor no portal MVPD. A autenticação deve ocorrer separadamente no portal MVPD.                                                                                                                                                    |           |                        |


<!--
>[!RELATEDINFORMATION]
>
>* MVPD Integration Features
>* Entitlement Flow
>* Platform / Device Requirements
-->
