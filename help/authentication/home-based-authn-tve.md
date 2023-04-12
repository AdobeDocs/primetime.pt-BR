---
title: Autenticação Baseada em Casa para TV em Todos os Lugares
description: Autenticação Baseada em Casa para TV em Todos os Lugares
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---


# Autenticação Baseada em Casa para TV em Todos os Lugares

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## O que é Autenticação Baseada em Casa? {#whatis-home-based-authn}

A HBA (Home Based Authentication, Autenticação Baseada em Casa) é um recurso da TV em Todos os Lugares que permite que os assinantes de TV por assinatura visualizem o conteúdo da TV on-line sem inserir credenciais MVPD em casa, melhorando significativamente a experiência do usuário do fluxo de autenticação.

Definição de Autenticação Baseada em Casa pelo Open Authentication Technology Committee (OATC): &quot;Autenticação automática interna é o processo pelo qual um MVPD/OVD usa características da rede doméstica (ou identificadores automaticamente acessíveis entre dispositivos na rede doméstica) para autenticar qual conta de assinante está associada a essa rede doméstica, de modo que os usuários não precisam inserir credenciais manualmente ao estabelecer uma sessão TVE para acessar conteúdo protegido TVE.&quot;



Para obter mais informações sobre HBA e padrões do setor, leia a seção [Casos de uso e requisitos da OATC](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} documentação e **Diretrizes de experiência do usuário do OATC para HBA**.

>[!NOTE]
>
>Alguns fluxos de HBA fazem parte do pacote Premium Workflow . Entre em contato com seu representante de vendas do Primetime, caso esteja interessado em usar essa funcionalidade.

## Por que o HBA é importante para você {#why-hba}

O HBA é importante porque praticamente remove a barreira de entrada para seus visualizadores que estão em casa e já têm assinatura a cabo. Além disso, a Autenticação com base em casa pode aumentar significativamente o engajamento dos visualizadores e oferecer uma melhor experiência do usuário para o seu conteúdo da TV em qualquer lugar.

Atualmente, quase metade das tentativas de entrar não são bem-sucedidas.

Depois que o HBA foi ativado por um dos 5 MVPDs principais, sua taxa de conversão de autenticação **aumentado em 40%** (de 45% a 63%)

![](assets/authn-conv-pre-post.png)

Além disso, abaixo você pode ver a taxa de conversão de entrada de um canal integrado com MVPDs diferentes: aqueles que habilitaram o HBA para ele e aqueles que não têm HBA. A taxa de conversão para aqueles com HBA é significativamente maior do que aqueles sem HBA.

![](assets/hba-vs-non-hba.png)

Seis meses depois de habilitar o HBA para a maioria dos canais integrados com esse MVPD, notamos um aumento de 82% em usuários únicos (o número de usuários acessando canais de TV em qualquer lugar por meio desse MVPD quase dobrou).

2w3Por outro lado, como você pode ver no gráfico abaixo, outros MVPDs que não habilitaram o HBA tiveram apenas um aumento de 26% nos usuários únicos nos últimos 6 meses.

![](assets/unique-visitors-incr.png)

De nossos dados, coletados 6 meses antes e 6 meses depois de habilitar o HBA, vimos um grande aumento no engajamento dos visualizadores para os canais que eram habilitados para o HBA. Praticamente os usuários de MVPDs que habilitaram o HBA tendem a assistir em média 30% mais conteúdo do que os usuários de MVPDs que não têm o HBA habilitado.

![](assets/user-engagement-increase.png)

## Suporte a HBA de autenticação do Primetime {#auth-hba-support}

Esta seção descreve o suporte de HBA fornecido pela autenticação do Primetime, o comportamento das plataformas de autenticação do Primetime nos fluxos de HBA e também oferece detalhes técnicos úteis para a implementação do HBA.

Recursos de autenticação do Primetime compatíveis com HBA

* Capacidade de definir diferentes TTLs de autenticação para autenticações de HBA versus autenticações não-HBA (também requer suporte a MVPD)
* Capacidade de selecionar automaticamente um MVPD (ignorar o seletor de MVPD) se a autenticação tiver expirado. Isso é útil principalmente quando os TTLs do HBA são pequenos.
* Capacidade de expor os programadores se a autenticação foi HBA ou não (também requer suporte MVPD)

### Experiência do usuário do HBA em plataformas de autenticação do Primetime {#hba-user-exp}

As tabelas a seguir fornecem informações sobre a experiência do usuário para as plataformas suportadas quando o HBA está habilitado e quando o HBA não está habilitado:

| Fluxo do usuário - Tipo de plataforma | swf, iOS, Android |
|---|---|
| Com HBA ativado | Quando os usuários estão em casa, eles são autenticados automaticamente. Depois que o token HBA AuthN expirar, os usuários serão automaticamente autenticados novamente. |
| Sem HBA | Os usuários são solicitados a selecionar seu MVPD e inserir suas credenciais, mesmo que estejam em casa.Depois que o token AuthN expirar, os usuários deverão inserir suas credenciais novamente. |

| Fluxo do usuário - Tipo de plataforma | js, Windows (nativo) |
|---|---|
| Com HBA ativado | Quando os usuários estão em casa, eles são autenticados automaticamente. Depois que o token HBA AuthN expirar, os usuários devem selecionar novamente seu MVPD no seletor e serão autenticados automaticamente. |
| Sem HBA | Os usuários são solicitados a selecionar seu MVPD e inserir suas credenciais, mesmo que estejam em casa. Depois que o token AuthN expirar, os usuários deverão inserir suas credenciais novamente. |

| Fluxo do usuário - Tipo de plataforma | REST API sem cliente (autenticação de segunda tela) |
|---|---|
| Com HBA ativado | Quando os usuários estão em casa e estão usando um aplicativo REST API sem cliente, eles são autenticados automaticamente no dispositivo de segunda tela depois de inserir o código de registro e selecionar o MVPD. Depois que o token HBA AuthN expirar, os usuários serão automaticamente reautenticados (no dispositivo de segunda tela). |
| Sem HBA | Os usuários são solicitados a selecionar seu MVPD e inserir suas credenciais, mesmo que estejam em casa. Depois que o token AuthN expirar, os usuários deverão inserir suas credenciais novamente. |

### Detalhes técnicos da implementação do HBA {#tech-details-hba}

#### Protocolo OAuth 2.0 {#oauth-2-protocol}

No fluxo do HBA para MVPDs integrados ao protocolo de autenticação OAuth 2.0, o MVPD emite um token de atualização e o Adobe emite um token de autenticação do HBA:

* O token de atualização tem um TTL determinado pelos requisitos comerciais do MVPD.
* TTL do token de autenticação do HBA **deve ser menor que ou igual a** o TTL do token de atualização.


*Descrição do fluxo de autenticação do HBA para o protocolo OAuth 2.0*


| Ações do usuário | Ações do sistema |
|---|---|
| O usuário navega até o site do programador. Ao tentar reproduzir um vídeo, o seletor de MVPD é exibido. O usuário seleciona o MVPD e clica no logon. | É realizada uma verificação de fundo. O MVPD aplica seu conjunto de regras para detecção de usuários (por exemplo, mapeie o endereço IP do usuário com o endereço MAC de modems provisionados pelo distribuidor ou caixas de decodificador conectadas por banda larga). |
| Uma tela, que persiste por cerca de 3 segundos, é exibida. Uma página intersticial pode ser exibida informando ao usuário que ele/ela está sendo conectado automaticamente usando sua conta MVPD. | <ol><li>O AccessEnabler, que é instalado no lado do programador, envia uma solicitação de autenticação (como uma solicitação HTTP) para o endpoint de Autenticação da Adobe Primetime.</li><li>O endpoint de Autenticação do Primetime redireciona a solicitação para o endpoint de autenticação do MVPD. <br />**Observação:** A solicitação contém a variável `hba_flag` parâmetro (tentativa HBA = true) que indica que o MVPD deve tentar a autenticação do HBA.</li><li>O endpoint de autenticação MVPD envia um código de autorização para o endpoint de Autenticação da Adobe Primetime.</li><li>A Autenticação Adobe Primetime usa o código de autorização para solicitar um token de atualização e um token de acesso do endpoint de token do MVPD.</li><li>O MVPD envia uma decisão de autenticação e a variável `hba_status` (true/false) no parâmetro da função `id_token`.</li><li>Uma chamada para o endpoint do perfil de usuário MVPD é enviada para expor a variável [chave hba_status nos metadados do usuário](/help/authentication/user-metadata-feature.md#obtaining).</li><li>O MVPD define o TTL do token de atualização para um valor acordado pelo MVPD e o Adobe define o TTL do token AuthN para um valor menor ou igual ao valor do token de atualização.</li></ol> |
| O usuário é autenticado e agora pode navegar pelo conteúdo da TV em qualquer lugar. | O token de autenticação é passado ao usuário que agora pode navegar com êxito no site do programador. |

#### Protocolo SAML {#saml-protocol}

Descrição do fluxo de autenticação do HBA para o protocolo de autenticação SAML

| Ações do usuário | Ações do sistema |
|---|---|
| O usuário navega até o site do programador. Ao tentar reproduzir um vídeo, o seletor de MVPD é exibido. O usuário seleciona o MVPD e clica no logon. | É realizada uma verificação de fundo. O MVPD aplica seu conjunto de regras para detecção de usuários (por exemplo, mapeie o endereço IP do usuário com o endereço MAC de modems provisionados pelo distribuidor ou caixas de decodificador conectadas por banda larga). |
| Uma tela, que persiste por cerca de 3 segundos, é exibida. Uma página intersticial pode ser exibida informando ao usuário que ele/ela está sendo conectado automaticamente usando sua conta MVPD. | <ol><li>O AccessEnabler, que é instalado no lado do programador, envia uma solicitação de autenticação (como uma solicitação HTTP) para o endpoint de Autenticação da Adobe Primetime.</li><li>O endpoint de Autenticação do Primetime redireciona a solicitação para o endpoint de autenticação do MVPD.</li><li>O MVPD deve enviar uma decisão de autenticação na forma de uma resposta SAML que deve conter o sinalizador HBA: hba_status (true/false).</li><li>Uma chamada para o endpoint do perfil de usuário MVPD é enviada para expor a variável [chave hba_status nos metadados do usuário](/help/authentication/user-metadata-feature.md#obtaining).</li></ol> |
| O usuário é autenticado e agora pode navegar pelo conteúdo da TV em qualquer lugar. | O token de autenticação é passado ao usuário que agora pode navegar com êxito no site do programador. |


## Como ativar o HBA {#how-to-activate-hba}

* **Protocolo OAuth:**
   * Para habilitar o HBA, consulte [Guia do usuário do painel do Primetime TVE](/help/authentication/tve-dashboard-user-guide.md)
* **Protocolo SAML:** A Autenticação Baseada em Casa é ativada no lado do MVPD. Nenhuma ação é necessária para o Programador ou o Adobe.
Para obter mais informações sobre os MVPDs que oferecem suporte à Autenticação Baseada em Página, consulte [Status do HBA para MVPDs](/help/authentication/hba-status-mvpds.md).

## Perguntas frequentes {#faqs}


**Pergunta:** Por que a separação entre a Autenticação Baseada em Casa e os protocolos SAML e OAuth2?

**Resposta:** O fluxo do HBA é diferente para os dois protocolos. Da perspectiva de um programador, não há necessidade de ação para garantir que o HBA esteja habilitado para MVPDs SAML, enquanto para MVPDs OAuth2, o HBA pode ser ativado ou desativado no Painel TVE do Primetime.



**Pergunta:** Os usuários precisam preencher um nome de usuário e senha na primeira vez que autenticarem quando o HBA estiver ativado?

**Resposta:** Não, o nome de usuário e a senha não são obrigatórios.



**Pergunta:** Como você faz cumprir os controles dos pais?

**Resposta 1:** O Adobe pode desativar o HBA para integrações com canais que precisam de aprovação do controle dos pais.

**Resposta 2:** O Adobe está trabalhando com o OATC em um documento UX que recomenda como configurar a experiência do HBA com controles dos pais.



**Pergunta:** Os provedores que oferecem suporte ao HBA têm janelas TTL mais curtas para o HBA do que têm para autenticação regular?

**Resposta:** A configuração TTL é configurável. Recomendamos configurar um TTL mais curto para tokens de autenticação do HBA, a fim de evitar manipulações incorretas.


## Informações úteis {#useful-info}

* [Recommendations de Acesso instantâneo (HBA)](http://www.ctamtve.com/instantaccess){target=_blank} - por CTAM
* [Exemplo de implementação do HBA no aplicativo do programador](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/HBA_Flow_Sample.pdf?dc=201604222139-1346){target=_blank} - por Adobe
   <!--* [Home Based Authentication User Experience Guidelines for TV Everywhere](http://oatc.us/Standards/DownloadRecommendedPractices.aspx){target=_blank} - by OATC-->
* [Casos de uso e requisitos de autenticação com base em casa](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} pela OATC
* [Infográfico de Autenticação Baseada em Casa](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AdobeNewsletterHBA.pdf?dc=201604260953-2640){target=_blank} - por Adobe
* [Autenticação usando o protocolo OAuth 2.0](/help/authentication/authn-oauth2-protocol.md)
* [Autenticação com MVPDs SAML](/help/authentication/authn-usecase.md)
* [Guia do usuário do painel do Primetime TVE](/help/authentication/tve-dashboard-user-guide.md)
* [Metadados do usuário hba_status](/help/authentication/user-metadata-feature.md#obtaining)



