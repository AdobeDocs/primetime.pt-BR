---
title: Guia da API REST (cliente para servidor)
description: Redefina o cliente do guia da API para o servidor.
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 1%

---


# Guia da API REST (cliente para servidor) {#rest-api-cookbook-client-to-server}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Visão geral {#overview}

Este documento fornece instruções passo a passo para a equipe de engenharia de um programador integrar um &quot;dispositivo inteligente&quot; (console de jogos, aplicativo de TV inteligente, set top box etc.) com a autenticação da Adobe Primetime usando serviços REST API. Essa abordagem cliente a servidor, que usa APIs REST em vez de um SDK do cliente, permite um suporte mais amplo a plataformas diferentes para as quais o desenvolvimento de um número significativo de SDKs exclusivos não seria viável. Para obter uma visão geral técnica de como a solução sem cliente funciona, consulte a [Visão geral técnica sem cliente](/help/authentication/rest-api-overview.md).


Essa abordagem requer dois componentes (aplicativo de transmissão e aplicativo AuthN) para concluir os fluxos necessários: inicialização, registro, autorização e fluxos de mídia de visualização no aplicativo de transmissão e o fluxo de autenticação no aplicativo AuthN.

## Componentes {#components}

Em uma solução cliente para servidor em funcionamento, os seguintes componentes estão envolvidos:

 

| Tipo | Componente | Descrição |
| --- | --- | --- |
| Dispositivo de transmissão | Aplicativo de transmissão | O aplicativo Programador que reside no dispositivo de transmissão do usuário e reproduz vídeo autenticado. |
|  | \[Opcional\] Módulo AuthN | se o dispositivo de transmissão tiver um agente de usuário (ou seja, navegador da Web), o módulo AuthN será responsável pela autenticação do usuário no IdP do MVPD. |
| \[Opcional\] Dispositivo AuthN | Aplicativo AuthN | se o dispositivo de transmissão não tiver um agente de usuário (ou seja, navegador da Web), o aplicativo AuthN será um aplicativo da Web programador acessado de um dispositivo de usuário separado usando um navegador da Web.  |
| Infraestrutura Adobe | Serviço Adobe Pass | Um serviço que se integra ao serviço MVPD IdP e AuthZ e fornece decisões de autenticação e autorização. |
| Infraestrutura MVPD | IdP MVPD | Um endpoint MVPD que fornece serviço de autenticação baseado em credenciais para validar a identidade do usuário. |
|  | Serviço AuthZ MVPD | Um terminal MVPD que fornece decisões de autorização com base em assinaturas do usuário, controles dos pais, etc. |

 

Os termos adicionais usados no fluxo são definidos na variável [Glossário](http://tve.helpdocsonline.com/adobe-pass-glossary).

## Fluxos{#flows}

### Registro dinâmico de cliente (DCR)

A Adobe Pass usa o DCR para proteger as comunicações do cliente entre um aplicativo programador ou servidor e os serviços da Adobe Pass. O fluxo de DCR é separado, dependente e de pré-requisito e pode ser encontrado aqui: http://tve.helpdocsonline.com/dynamic-client-registration


### Fluxos do aplicativo de transmissão (dispositivo inteligente)

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/clientless_1st_screen_updated.PNG)

 

#### Fluxo de inicialização

1. Seu aplicativo é iniciado e carrega a interface inicial.

2. Obter / gerar uma ID de dispositivo.

3. Emita uma chamada Check-authentication para ver se o dispositivo já está autenticado.  Por exemplo: [`<SP_FQDN>/api/v1/checkauthn [device ID]`](/help/authentication/check-authentication-token.md)

4. Se a variável `checkauthn` chamada bem-sucedida, prossiga para o Fluxo de autorização da Etapa 2 em diante.  Se falhar, inicie o Fluxo de registro.

 

#### Fluxo de registro

1. Obtenha um código de registro e URL para o usuário usar para acessar seu aplicativo de logon de segunda tela e apresente-os ao usuário:

   a. Envie uma solicitação POST ao Serviço de código de registro do Adobe, transmitindo uma ID de dispositivo com hash e um &quot;URL de registro&quot;.  Por exemplo: [`<REGGIE_FQDN>/reggie/v1/[requestorId]/regcode [device ID]`](/help/authentication/registration-code-request.md)

   b. Apresentar o código de registro e o URL retornados ao usuário.

   c. Instrua o usuário a alternar para um dispositivo compatível com a Web, navegue até o URL e insira o código de registro.

 

#### Fluxo de autorização

1. O usuário retorna do aplicativo de segunda tela e pressiona o botão &quot;Continuar&quot; no dispositivo. Como alternativa, você poderia implementar um mecanismo de pesquisa para verificar o status de autenticação, mas a autenticação da Adobe Primetime recomenda o método do botão Continuar durante a pesquisa. <!--(For information on employing a "Continue" button versus polling the Adobe Primetime authentication backend server, see the Clientless Technical Overview: Managing 2nd-Screen Workflow Transition.)--> Por exemplo: [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md)

2. Envie uma solicitação GET ao serviço de autorização de autenticação da Adobe Primetime para iniciar a autorização. Por exemplo: `<SP_FQDN>/api/v1/authorize [device ID, Requestor ID, Resource ID]`

<!-- end list -->

- Se a resposta indicar sucesso: O usuário tem um token AuthN válido E o usuário está autorizado a assistir a mídia solicitada (há um token AuthZ válido para esse usuário).

- Se a resposta indicar falha: Examine a Exceção acionada para determinar seu tipo (AuthN, AuthZ ou algo diferente):

   - Se foi um erro de AuthN, reinicie o Fluxo de registro.

   - Se foi um erro de AuthZ, o usuário não está autorizado a assistir à mídia solicitada e algum tipo de mensagem de erro deve ser exibida para o usuário.

   - Se houver algum outro erro (erro de conexão, erro de rede etc.) em seguida, exibir uma mensagem de erro apropriada para o usuário.

 

#### Exibir fluxo de mídia

1. Apresente opções de mídia. O usuário seleciona a mídia a ser exibida.

2. A mídia está protegida?

   a. Seu aplicativo verifica se a mídia está protegida.

   b. Se a mídia estiver protegida, o aplicativo inicia o fluxo de autorização (AuthZ) acima.

   c. Se a mídia não estiver protegida, reproduza a mídia para o usuário.

3. Reprodução da mídia.


### Fluxo do aplicativo AuthN (segunda tela)

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/smart_dev_second_flow.png)

1. Obtenha uma lista de MVPDs para este usuário. Por exemplo: [`<SP_FQDN>/api/v1/config/[requestorID]`](/help/authentication/provide-mvpd-list.md)

1. Inicie o fluxo de autenticação.  Por exemplo: [`<SP_FQDN>/api/v1/authenticate [requestorID, MVPD ID, Redirect URL, Domain name, Registration Code, "noflash=true"]`](/help/authentication/initiate-authentication.md)

1. Verifique se a autenticação foi bem-sucedida.  Por exemplo: [`<SP_FQDN>/api/v1/checkauthn/[registration code][requestor ID]`](/help/authentication/check-authentication-token.md)

1. Envie o usuário de volta ao aplicativo Smart Device para concluir o fluxo de autorização.

 

## Platform SSO {#platform-sso}

Algumas plataformas fornecem suporte dedicado para o Logon único (SSO). Os detalhes de implementação podem ser encontrados para cada plataforma:

- [Apple SSO](http://tve.helpdocsonline.com/rest-api-apple-sso)
- Amazon SSO

## TempPass and Promotional TempPass for REST API {#temppass}

Para implementações TempPass e Promotional TempPass em que o usuário não é obrigado a inserir credenciais, a autenticação pode ser implementada diretamente no Aplicativo de transmissão. 

**Para usar essa API, o aplicativo de transmissão precisa garantir a exclusividade da ID do dispositivo, pois está sendo usada para identificar o token, juntamente com os dados adicionais opcionais.**


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/Free%20preview%20option.png?dc=201612071020-0)

### Informações relacionadas {#related}

- [Referência da API REST](/help/authentication/rest-api-reference.md)
