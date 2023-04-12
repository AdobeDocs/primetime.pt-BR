---
title: Autenticação usando o protocolo OAuth 2.0
description: Autenticação usando o protocolo OAuth 2.0
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# Autenticação usando o protocolo OAuth 2.0

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview}

Embora o SAML ainda seja o principal protocolo usado para autenticação pelos MVPDs dos EUA e empresas em geral, há uma clara tendência para mudar para o OAuth 2.0 como o protocolo de autenticação principal. O protocolo OAuth 2.0 (https://tools.ietf.org/html/rfc6749) foi desenvolvido principalmente para sites de consumo e foi rapidamente adotado por gigantes da Internet como Facebook, Google e Twitter.

O OAuth 2.0 é extremamente bem-sucedido e isso fez com que as empresas atualizassem lentamente suas infraestruturas para suportá-lo.



## Vantagens de migrar para o OAuth 2.0 {#adv-oauth2}

Em um alto nível, o protocolo OAuth 2.0 oferece a mesma funcionalidade que o protocolo SAML, mas há algumas distinções importantes.

Uma delas é o fato de que o fluxo do token de atualização pode ser usado como uma maneira de atualizar a autenticação nos bastidores. Isso permite que o IdP (os MVPDs, neste caso) mantenha o controle enquanto ainda permite uma boa experiência do usuário, pois o usuário não é mais obrigado a fazer logon com frequência devido a questões de segurança.

O protocolo também oferece mais flexibilidade em termos de dados expostos como um provedor de serviços. Agora, é possível usar os tokens para acessar outras APIs e obter informações adicionais. Isso, por sua vez, resulta em um protocolo &quot;chattier&quot; para casos de uso de TVE, mas permite a flexibilidade necessária para fluxos de trabalho complexos.





## Requisitos para alternar para OAuth 2.0 {#oauth-req}

Para ser compatível com a autenticação com o OAuth 2.0, um MVPD precisa atender aos seguintes pré-requisitos:

Em primeiro lugar, o MVPD deve certificar-se de que suporta o *[Concessão do código de autorização](https://oauthlib.readthedocs.io/en/latest/oauth2/grants/authcode.html) fluxo.

Depois de confirmar que suporta o fluxo, o MVPD deve fornecer-nos as seguintes informações:

* o ponto final de autenticação
   * o ponto final fornecerá o código de autorização que será posteriormente usado em troca do token de atualização e acesso
* o ponto final /token
   * isso fornecerá o token de atualização e o token de acesso
   * o token de atualização precisa ser estável (ele não deve ser alterado sempre que solicitamos um novo token de acesso
   * o MVPD precisa permitir vários tokens de acesso ativos para cada token de atualização
   * esse ponto final também trocará um token de atualização para um token de acesso
* precisamos de um **ponto final para perfil do usuário**
   * esse ponto final fornecerá a userID, que precisa ser exclusiva para uma conta e não deve conter informações pessoais identificáveis
* o **/logout** ponto final (opcional)
   * A autenticação da Adobe Primetime será redirecionada para esse ponto final, fornecendo ao MVPD um URI de redirecionamento; nesse ponto final, o MVPD pode limpar os cookies na máquina cliente ou aplicar qualquer lógica desejada para logout
* é altamente recomendável ter suporte para clientes autorizados (aplicativos clientes que não acionam uma página de autorização do usuário)
* também precisaremos:
   * **clientID** e **segredo do cliente** para as configurações de integração
   * **tempo de vida** (TTL) valores para o token de atualização e o token de acesso
   * Podemos fornecer ao MVPD um URI de retorno de chamada e de logout de autorização. Além disso, se necessário, podemos fornecer aos MVPDs uma lista de IPs a serem incluídos na lista de permissões nas configurações do firewall.


## Fluxo de autenticação {#authn-flow}

No fluxo de autenticação, a autenticação da Adobe Primetime se comunicará com o MVPD no protocolo selecionado na configuração. O fluxo OAuth 2.0 é ilustrado na figura abaixo:



![Diagrama para mostrar o fluxo de Autenticação na Autenticação de Adobe que se comunica com o MVPD no protocolo selecionado na configuração.](assets/authn-flow.png)

**Figura 1: Fluxo de autenticação do OAuth 2.0**



## Solicitação e resposta de autenticação {#authn-req-response}

Em resumo, o fluxo de autenticação para MVPDs compatíveis com o protocolo OAuth 2.0 segue estas etapas:

1. O usuário final navega até o site do Programador e seleciona fazer logon com suas credenciais do MVPD
1. O AccessEnabler instalado no lado do Programador com enviar uma solicitação de Autenticação na forma de uma solicitação HTTP para o endpoint de autenticação da Adobe Primetime, que o endpoint de autenticação da Adobe Primetime redireciona para o endpoint de autorização MVPD.
1. O endpoint de autorização MVPD envia um código de autorização para o endpoint de autenticação da Adobe Primetime
1. A autenticação da Adobe Primetime usa o código de autorização recebido para solicitar um token de atualização e um token de acesso do endpoint de token do MVPD
1. Uma chamada para buscar informações e metadados do usuário pode ser enviada para o endpoint do perfil do usuário caso as informações do usuário não estejam incluídas no token
1. O token de autenticação é passado ao usuário final que agora pode navegar com êxito no site do Programador

   >[!NOTE]
   >
   >O token de atualização é usado para obter um novo token de acesso depois que o token de acesso atual se tornar inválido ou expirar.


>[!IMPORTANT]
>
>O token de atualização não deve mudar quando for trocado por um token de acesso.

Essa limitação provém dos fluxos do cliente que não permitem que o servidor atualize o AuthNToken que, para o protocolo OAuth 2.0, também contém o token de atualização.

Um fluxo de autorização típico realiza uma troca do token de atualização salvo no AuthNToken para um token de acesso que é usado subsequentemente para executar a chamada de autorização no nome do usuário que foi autenticado em primeiro lugar. Se o Servidor de Autorização (o MVPD) alterar o token de atualização e invalidar o antigo, não poderemos atualizar o AuthNToken válido. Por isso, os MVPDs precisam suportar tokens de atualização estáveis para poder configurar integrações do OAuth 2.0 para eles.


## Migração do SAML para OAuth 2.0 {#saml-auth2-migr}

A migração das integrações de SAML para OAuth 2.0 será realizada pelo Adobe e pelo MVPD. Não há necessidade de qualquer alteração técnica no lado do programador, embora o programador possa querer verificar/testar a associação de marcas na página de logon do MVPD. Do ponto de vista do MVPD, os pontos finais e outras informações solicitadas no Oauth 2.0 são necessários.

Para **preserve SSO**, os usuários que já têm um token de autenticação obtido por meio do SAML ainda serão considerados autenticados e suas solicitações serão roteadas por meio da integração SAML antiga.

Do ponto de vista técnico:

1. O Adobe habilitará uma integração OAuth 2.0 entre o programador e o MVPD, SEM excluir a integração SAML.
1. Após a ativação, todos os novos usuários usarão os fluxos do OAuth 2.0.
1. Os usuários já autenticados, que já têm um token AuthN local que contém o subject-id do SAML, serão encaminhados automaticamente pelo Adobe por meio da integração do SAML.
1. Para os usuários na etapa 3, depois que o token AuthN gerado pelo SAML expirar, o Adobe os tratará como novos usuários e se comportará como os usuários na etapa 2.
1. O Adobe analisará os padrões de uso para determinar o momento em que a integração do SAML pode ser desativada com segurança.

