---
title: Glossário
description: Glossário
exl-id: e64a94f6-7460-4aa8-8d6b-e0553ba1e4ec
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# Glossário {#glossary}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## AccessEnabler {#accessEnabler}

O componente cliente da autenticação do Adobe Primetime. A autenticação do Adobe Primetime fornece uma biblioteca AccessEnabler para cada plataforma compatível.

## AuthN {#authn}

Usado como abreviação para &quot;autenticação&quot;, como em &quot;AuthN Token&quot; ou &quot;Fluxo AuthN&quot;.


## Token de autenticação{#authn-token}

Token de autenticação, gerado pela autenticação da Adobe Primetime depois que um usuário é autenticado com êxito com um MVPD. Dependendo da plataforma de integração do Programador, o token é armazenado no dispositivo do usuário ou nos servidores de autenticação da Adobe Primetime.

## AuthZ {#authz}

Usado como abreviação para &quot;autorização&quot;, como em &quot;AuthZ Token&quot; ou &quot;Fluxo AuthZ&quot;.

## Token de autorização {#authz-token}

Token de autorização, gerado pela autenticação da Adobe Primetime depois que um usuário é autorizado a exibir conteúdo protegido. O token de autenticação é armazenado nos servidores de autenticação da Adobe Primetime e usado para gerar um [Token de mídia de vida curta](#short-lived-token).

## ID do canal (obsoleto) {#channel_id}

Termo anterior para a ID do recurso.

## API sem cliente {#clientless-api}

Uma solução de integração de autenticação da Adobe Primetime que emprega serviços da Web em vez do componente do cliente AccessEnabler.

## ID do dispositivo {#device-id}

Identifica exclusivamente um dispositivo (como um telefone, tablet etc.) na autenticação do Adobe Primetime. Essa ID é obtida/fornecida pelo aplicativo do programador.


## Fluxo de direitos{#entitlement_flow}

O termo usado na documentação de autenticação do Adobe Primetime para se referir a todo o processo de registro de um dispositivo/usuário com autenticação do Adobe Primetime, autenticação de um usuário com um MVPD, autorização de um recurso para um usuário e logout de um usuário.


## GUID {#guid}

Consulte [ID de usuário](#user-id).

## IdP {#idp}

Identificar provedor; sinônimo de MVPD no contexto de uma função de MVPD em uma integração de autenticação da Adobe Primetime. (Os clientes devem verificar sua identidade por meio da página de logon do provedor de TV paga.)

## Verificador de token de mídia {#media-token-verifier}

Uma biblioteca fornecida por Adobe usada pelos programadores para verificar o token de mídia de vida curta gerado pela autenticação Adobe Primetime após a conclusão bem-sucedida de um fluxo de direitos.

## MVPD {#mvpd}

Distribuidor de programação de vídeo multicanal; sinônimo de &quot;Pay TV Provider&quot;.

## ID MVPD {#mvpd-id}

Consulte [ID de usuário](#user-id).

## ID do Parceiro {#partner-id}

Um identificador que o Adobe passa para MVPDs, que o usam para identificar em nome de quem a autenticação da Adobe Primetime está solicitando autenticação. Às vezes, é usado para configurar suas interfaces para programadores específicos, às vezes, é o mesmo em todos os programadores, depende das necessidades do MVPD.

## Provedor de TV por Assinatura {#pay-tv-provider}

Sinônimo de [MVPD](#mvpd).

## Programador {#programmer}

Sinônimo de &quot;provedor de conteúdo&quot;, &quot;conta&quot;, &quot;canal&quot;, &quot;provedor de serviço&quot;, &quot;marca&quot; e assim por diante.

## Proxy MVPD {#proxy-mvpd}

Um MVPD que fornece serviços de identidade para outros MVPDs; diretamente integrado à autenticação da Adobe Primetime.

## MVPD com proxy {#proxied-mvpd}

Um MVPD que não tenha uma integração direta com o SP do Adobe, mas seja integrado por meio de um MVPD de proxy.

## ID do Solicitante {#requestor-id}

Identifica exclusivamente um [Programador](#programmer) (uma conta, marca, canal ou propriedade) na autenticação da Adobe Primetime. Essa ID é determinada entre o Programador e o Adobe durante a configuração inicial da conta. Na Web, a ID do solicitante está associada a um conjunto de domínios da lista de permissões; todas as chamadas que usam uma ID de um domínio externo serão recusadas. Os programadores também usam a ID do solicitante para análise. Normalmente, há apenas uma ID de solicitante por programador. Um recurso adicional relacionado à ID do solicitante é que o programador deve fornecer um certificado público ao Adobe, já que a chamada da API setRequestor espera que dados criptografados sejam enviados, usados para autenticar o programador no sistema de autenticação da Adobe Primetime.

## ID do recurso {#resource-id}

Uma cadeia de caracteres ou um recurso mRSS que identifica uma [Programador](#programmer) para MVPDs. É acordado entre o Programador e os MVPDs; a autenticação do Adobe Primetime transmite a ID do recurso por meio do intocado, portanto, deve ser a mesma para todos os MVPDs. Um Programador pode usar várias IDs de recursos, desde que os MVPDs estejam cientes do que cada ID representa.

## SessionGUID {#sessionGUID}

Consulte [ID de usuário](#user-id).

## Token de mídia de vida curta {#short-lived-token}

Esse token é gerado pela autenticação da Adobe Primetime após a conclusão bem-sucedida do processo de qualificação para um usuário específico. O token é passado para o Programador, que usa o Verificador de token de autenticação do Adobe Primetime no Token de mídia de vida curta para verificar a segurança do processo de qualificação.

## Dispositivo inteligente {#smart-device}

Um termo usado em toda a documentação de autenticação do Adobe Primetime para se referir a decodificadores de sinais, consoles de jogos e TVs inteligentes. Esses são dispositivos que têm recursos de rede, mas não são capazes de renderizar páginas da Web.

## SP{#sp}

Prestador de serviços; geralmente refere-se ao *função* de SP, executada pela autenticação Adobe Primetime, atuando em nome de um Programador em uma integração com um [MVPD](#mvpd).

## Temp Pass (Aprovação temporária) {#temp-pass}

Um recurso que permite aos programadores fornecer acesso gratuito temporário a conteúdo pago. O acesso é por solicitante, por um período especificado pelo programador.

## TTL {#ttl}

Tempo De Vida. Esse é o período especificado em que um token é válido.

## TVE {#tve}

Televisão em todos os lugares.

## ID de usuário {#user-id}

Identifica exclusivamente o usuário de um aplicativo do programador, mas é originário do MVPD. Disponível em diferentes formulários para diferentes casos de uso. Consulte [Compreender IDs de usuário na visão geral do programador](/help/authentication/programmer-overview.md#user-ids).

## Lista de permissões {#whitelist}

Uma lista de domínios designados como legítimos para fins de comunicação com a autenticação da Adobe Primetime.

## Token XSTS {#xsts-token}

Um token de segurança emitido pelo Microsoft para desenvolvimento de aplicativo de console Xbox, usado na integração de autenticação Xbox/Adobe Primetime.
