---
title: Glossário
description: Glossário
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Glossário {#glossary}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## AccessEnabler {#accessEnabler}

O componente cliente da autenticação da Adobe Primetime. A autenticação da Adobe Primetime fornece uma biblioteca do AccessEnabler para cada plataforma compatível.

## AuthN {#authn}

Usado como abreviado para &quot;autenticação&quot;, como em &quot;Token de AuthN&quot; ou &quot;Fluxo de AuthN&quot;.


## Token de AuthN{#authn-token}

Token de autenticação, gerado pela autenticação da Adobe Primetime depois que um usuário é autenticado com êxito com um MVPD. Dependendo da plataforma de integração do Programador, o token é armazenado no dispositivo do usuário ou nos servidores de autenticação da Adobe Primetime.

## AuthZ {#authz}

Usado como abreviado para &quot;autorização&quot;, como em &quot;Token de AuthZ&quot; ou &quot;Fluxo de AuthZ&quot;.

## Token de AuthZ {#authz-token}

Token de autorização, gerado pela autenticação do Adobe Primetime após um usuário ter sido autorizado a exibir conteúdo protegido. O token AuthZ é armazenado nos servidores de autenticação da Adobe Primetime e é usado para gerar um [Token de mídia de duração curta](#short-lived-token).

## ID do canal (obsoleto) {#channel_id}

Termo anterior para ID do recurso.

## API sem cliente {#clientless-api}

Uma solução de integração de autenticação da Adobe Primetime que emprega serviços da Web em vez do componente de cliente AccessEnabler.

## ID do dispositivo {#device-id}

Identifica exclusivamente um dispositivo (como um telefone, tablet etc.) na autenticação da Adobe Primetime. Essa ID é obtida/fornecida pelo aplicativo do Programador.


## Fluxo de direitos{#entitlement_flow}

O termo usado na documentação de autenticação do Adobe Primetime para se referir a todo o processo de registro de um dispositivo/usuário com autenticação Adobe Primetime, autenticação de um usuário com um MVPD, autorização de um recurso para um usuário e logout de um usuário.


## GUID {#guid}

Consulte [ID de usuário](#user-id).

## IdP {#idp}

Identificar Provedor; sinônimo de MVPD no contexto da função de um MVPD em uma integração de autenticação da Adobe Primetime. (Os clientes devem verificar sua identificação por meio da página de logon do Provedor de TV por assinatura.)

## Verificador de token de mídia {#media-token-verifier}

Uma biblioteca fornecida pelo Adobe usada pelos Programadores para verificar o token de mídia de curta duração gerado pela autenticação da Adobe Primetime após a conclusão bem-sucedida de um fluxo de direito.

## MVPD {#mvpd}

Distribuidor de programação de vídeo multicanal; sinônimo de &quot;Pay TV Provider&quot;.

## ID do MVPD {#mvpd-id}

Consulte [ID de usuário](#user-id).

## ID do parceiro {#partner-id}

Um identificador que o Adobe transmite para os MVPDs, que o usam para identificá-lo em cujo nome a autenticação da Adobe Primetime está solicitando autenticação. Às vezes, é usado para configurar suas interfaces de usuário para determinados programadores, às vezes é o mesmo em todos os programadores, depende das necessidades do MVPD.

## Fornecedor de TV por Pagamento {#pay-tv-provider}

Sinônimo de [MVPD](#mvpd).

## Programador {#programmer}

Sinônimo de &quot;provedor de conteúdo&quot;, &quot;conta&quot;, &quot;canal&quot;, &quot;provedor de serviços&quot;, &quot;marca&quot; e assim por diante.

## MVPD do Proxy {#proxy-mvpd}

Um MVPD que preste serviços de identidade a outros MVPD; diretamente integrada com a autenticação da Adobe Primetime.

## MVPD Proxito {#proxied-mvpd}

Um MVPD que não tem uma integração direta com o SP do Adobe, mas é integrado por meio de um MVPD de Proxy.

## ID do solicitante {#requestor-id}

Identifica exclusivamente uma [Programador](#programmer) (uma conta, marca, canal ou propriedade) na autenticação da Adobe Primetime. Essa ID é determinada entre o Programador e o Adobe durante a configuração inicial da conta. Na Web, a ID do solicitante está associada a um conjunto de domínios da lista de permissões; todas as chamadas que usam uma ID de um domínio externo serão recusadas. Os programadores também usam a ID do solicitante para o Analytics. Geralmente, há apenas uma ID de Solicitante por Programador. Um recurso adicional relacionado à ID do Solicitante é que o Programador deve fornecer ao Adobe um certificado público, já que a chamada da API setRequestor espera que os dados criptografados sejam enviados, usados para autenticar o Programador no sistema de autenticação do Adobe Primetime.

## ID do recurso {#resource-id}

Uma string ou recurso mRSS que identifica um [Programador](#programmer) para MVPDs. É acordado entre o programador e os MVPD; A autenticação da Adobe Primetime passa a ID do recurso por intocado, portanto, deve ser a mesma para todos os MVPDs. Um programador pode usar várias IDs de recurso, desde que os MVPDs estejam cientes do que cada ID representa.

## SessionGUID {#sessionGUID}

Consulte [ID de usuário](#user-id).

## Token de mídia de duração curta {#short-lived-token}

Esse token é gerado pela autenticação da Adobe Primetime após a conclusão bem-sucedida do processo de direito de um usuário específico. O token é transmitido ao Programador, que usa o Verificador de Token de autenticação da Adobe Primetime no Token de mídia de duração curta para verificar a segurança do processo de direito.

## Dispositivo inteligente {#smart-device}

Um termo usado em toda a documentação de autenticação da Adobe Primetime para se referir a decodificadores de sinais, consoles de jogos e TVs inteligentes. Esses são dispositivos que têm recursos de rede, mas não são capazes de renderizar páginas da Web.

## SP{#sp}

Prestador de serviços; isto geralmente se refere ao *função* do SP, reproduzido pela autenticação da Adobe Primetime, atuando em nome de um programador em uma integração com um [MVPD](#mvpd).

## Aprovação temporária {#temp-pass}

Um recurso que permite aos programadores fornecer acesso gratuito temporário para pagar conteúdo. O acesso é por Solicitante, por um período especificado pelo Programador.

## TTL {#ttl}

Hora De Viver. Este é o período especificado para a validade de um token.

## TVE {#tve}

Televisão em qualquer lugar.

## ID de usuário {#user-id}

Identifica exclusivamente o usuário de um aplicativo do Programador, mas é originário do MVPD. Disponível em diferentes formulários para diferentes casos de uso. Consulte [Como entender as IDs de usuário na visão geral do programador](/help/authentication/programmer-overview.md#user-ids).

## Lista de permissões {#whitelist}

Uma lista de domínios designados como legítimos para fins de comunicação com a autenticação da Adobe Primetime.

## Token XSTS {#xsts-token}

Um token de segurança emitido pelo Microsoft para o desenvolvimento de aplicativo do console Xbox, usado na integração de autenticação Xbox/Adobe Primetime.
