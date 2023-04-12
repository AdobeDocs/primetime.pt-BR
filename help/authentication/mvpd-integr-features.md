---
title: Recursos de integração do MVPD
description: Recursos de integração do MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 2%

---


# Recursos de integração do MVPD

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#mvpd-int-features-overview}

A autenticação Adobe Primetime suporta os padrões emergentes para TV em qualquer lugar. Ele é compatível com o **Especificação CableLabs OLCA (Online Content Access)**, que fornece requisitos técnicos e arquitetura para a entrega de vídeo a um cliente de TV paga de fontes online. A Adobe participou do projeto conjunto de testes interopcionais CableLabs em junho de 2011 e aprovou o processo de teste para a implementação de um Provedor de serviços.  O Adobe também é um membro ativo do **OATC (Open Authentication Technical Consortium)** e participa em vários projetos de especificação dos subcomités no âmbito desse organismo.

Após ter descrito a conformidade com a autenticação do Primetime OLCA e participação do Adobe no OATC, também é importante observar que a autenticação do Primetime é na verdade &quot;agnóstica de protocolo&quot;.  Mas nesta fase da era TVE, a autenticação do Primetime está definitivamente orientada para os padrões OLCA.  Os padrões delineiam as maneiras acordadas para os diferentes players TVE (Programadores, MVPDs e Provedores de Serviços) implementarem recursos TVE. Muitos desses recursos estão listados nas tabelas abaixo, com links para páginas relacionadas que fornecem detalhes e exemplos de como implementar os recursos.

As informações nas tabelas têm como objetivo direcionar o processo de integração de autenticação do Primetime para uma funcionalidade consistente em todas as integrações MVPD. A coluna de prioridade classifica os recursos em A, B e C:

* R - Esses são recursos &quot;devem ter&quot; para a implantação inicial de uma integração.
* B - Esses são aprimoramentos importantes na integração inicial, a serem adicionados após a implantação inicial.
* C - São aprimoramentos adicionais à integração que podem ser implementados após os requisitos &quot;B&quot;.


## 1. Principais recursos funcionais {#core-func-features}


| Não. | Recurso | Descrição | Prioridade | Notas |
|------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1.1 | [Logon iniciado pelo programador](/help/authentication/authn-oauth2-protocol.md) | O visualizador seleciona o MVPD e inicia o fluxo de autenticação (AuthN) do site ou aplicativo da marca do programador. | A+ |  |
| 1.2 | [Autorização baseada em canal](/help/authentication/authz-usecase.md) | Depois de autenticada, a autorização (AuthZ) pode ocorrer em segundo plano, com a transmissão de apenas um identificador de canal de rede e um identificador de usuário ao MVPD. | A+ |  |
| 1.3 | Persistência de UserID | O MVPD fornece um UserID ofuscado e persistente. | A |  |
| 1.4 | [Suporte para logon único](/help/authentication/sso-support.md) | O visualizador faz logon com o MVPD no site de uma marca e pode então ir para outra marca e não ser solicitado a fazer logon novamente. A sessão AuthN é compartilhada entre as marcas. O suporte SSO é para sites e aplicativos móveis/de dispositivo.  Para MVPDs, isso requer retornar um ID de usuário ou algum outro token de usuário que possa ser usado para AuthZ em marcas. | A |  |
| 1.5 | Experiência do usuário de logon (UX) otimizada pelo dispositivo | O MVPD suporta o redimensionamento da tela de logon para que se ajuste às dimensões do dispositivo que a exibição está usando. | A |  |
| 1.6 | Logotipo padrão do Seletor MVPD | O MVPD fornece um URL para um logotipo padrão de dimensões apropriadas (112x33 pixels). | A | O logotipo deve ser hospedado pelo MVPD e deve ser armazenado em cache pelo CDN. |
| 1.7 | [Escopo do Provedor de Serviços](/help/authentication/serv-provider-scoping.md) | O MVPD suporta a transmissão do identificador de marca (valor do Solicitante) na solicitação AuthN. | A- | Isso habilita uma experiência de logon específica do Provedor de serviços. |
| 1.8 | [Autorização de vários canais](/help/authentication/mvpd-preflight-authz.md#preflight-multich-authz) | O MVPD é compatível com um Programador enviando vários canais em uma única solicitação de autorização. | B+ |  |
| 1.9 | Autenticação baseada em iFrame ou &quot;Pop-up JS&quot; | O Programador pode integrar o fluxo de logon em um iFrame ou experiência pop-up, em vez de um redirecionamento HTTP. | B |  |
| 1.10 | [Logout iniciado pelo programador](/help/authentication/usecase-mvpd-logout.md) | O visualizador tem uma sessão autenticada tanto no site ou no aplicativo do programador quanto no MVPD. O visualizador pode iniciar um logout federado no site do programador e o logout também limpa a sessão no portal MVPD. | B | Garante que os computadores compartilhados sejam mais protegidos contra uso indevido da perspectiva do Programador. |
| 1.11 | [Mensagens de erro de autorização personalizada](/help/authentication/error-reporting.md) | O MVPD passa sua própria sequência de erro personalizada, que é apropriada para o Site ou Aplicativo federado do Programador exibir para o usuário. | B | Permite cenários de venda adicional |
| 1.12 | **Metadados do usuário na resposta de autenticação** | A resposta MVPD AuthN pode incluir metadados do usuário que atuam como uma dica para personalização da experiência do usuário durante o fluxo de direito. Esse requisito permite que o controle dos pais dê dicas do MVPD ao programador. | B- |  |
| 1.13 | Autenticação iniciada pelo MVPD | O visualizador conclui uma sessão AuthN bem-sucedida no portal MVPD e, em seguida, navega até o site TVE do programador. O usuário não é solicitado para o seletor MVPD e é autenticado automaticamente. | B- |  |
| 1.14 | Escopo da ID do usuário | A ID de usuário do MVPD deve ocorrer de duas formas: uma com escopo para Programadores e a outra com escopo Adobe para todo o caso, para fraude.  Isso permite que o Adobe compartilhe a ID de usuário MVPD com escopo de programador sem encriptação/ofuscação adicionais. | C |  |
| 1.15 | Autorização baseada em ativos | Quando o AuthN for concluído, o AuthZ poderá ocorrer em segundo plano, transmitindo dados estruturados que podem incluir rede, exibição, ativo, classificação de controle parental e muito mais, conforme necessário. Isso permite o controle dos pais em cada chamada AuthZ do Programador para o MVPD. | C |  |
| 1.16 | Logout iniciado pelo MVPD | O visualizador tem uma sessão autenticada no site ou aplicativo do programador e com o MVPD. O visualizador pode iniciar um logout federado no site do MVPD que também limpa a sessão em todos os sites do programador federado. | C |  |
| 1.17 | Obrigações de autorização | O MVPD fornece condições adicionais na resposta AuthZ, como registro ou uma classificação de controle parental (OLCA) atualizada. | C |  |
| 1.18 | Contexto de endereço IP | O MVPD requer transmitir explicitamente o endereço IP. Para AuthZ, onde as chamadas são do lado do servidor, isso fornece ao MVPD informações de rastreamento de fraude sobre de onde o usuário vem na chamada AuthZ. | C |  |
| 1.19 | Valor TTL (Token Persistence Time-to-live) definido dinamicamente | O MVPD é capaz de definir o TTL do token de autenticação do Primetime dinamicamente por meio de propriedades na resposta, de modo que o Adobe esteja fora do loop para alterações de TTL. | C- |  |
| 1.20 | Tipo de dispositivo | O MVPD suporta a transmissão do tipo de dispositivo na solicitação AuthN ou AuthZ. Essa propriedade informa o MVPD sobre a natureza do dispositivo no qual o conteúdo será consumido, para que ele possa ajustar o TTL do token AuthN ou AuthZ para estar em conformidade com suas próprias considerações de segurança do dispositivo. | C- | Isso é útil para a plataforma sem cliente, onde pode ser difícil expor cada tipo de dispositivo como uma configuração de configuração no lado da autenticação do Primetime. |



## 2. Características operacionais {#operational-features}

| Não | Recurso | Descrição | Prioridade | Notas |
|-----|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|-------|
| 2.1 | 24 horas por dia, 7 dias por semana | Um acordo MVPD para se esforçar 24 horas por dia, 7 dias por semana e para medir isso ao longo do tempo. | A |  |
| 2.2 | Testar Credenciais Para Cada Programador | O MVPD fornece contas de teste separadas para cada Programador. | A |  |
| 2.3 | Expiração do Certificado e Plano de Programação de Renovação | Um plano documentado por MVPD com uma agenda para garantir que os certificados SAML estejam atualizados. | A- |  |
| 2.4 | Latência Média Abaixo De 250 Ms/Resposta | Um acordo MVPD para procurar baixa latência e para medir isso ao longo do tempo. | A- |  |
| 2.5 | Logotipo do Seletor de MVPD da Hospedagem | O MVPD precisa hospedar seu próprio logotipo e deve ser protegido pelo armazenamento em cache da CDN. | B |  |
| 2.6 | Plano de escalonamento de suporte | Um plano de escalonamento documentado do MVPD que é atualizado e revisado pelo menos trimestralmente. | A |  |
| 2.7 | Plano de proteção contra interrupção | Um co-plano MVPD com medidas de degradação de Adobe on que podem ser usadas geralmente, conforme necessário. | B |  |
| 2.8 | Manter endpoints de armazenamento temporário e produção separados | Um teste de integração MVPD que não requer falsificação de arquivo de host para testar a integração de preparo. | B |  |
| 2.9 | Endpoint de controle de qualidade adicional | O MVPD mantém uma integração de IdP de controle de qualidade adicional para o desenvolvimento conjunto de novos recursos.  Se isso for suportado, será menos provável que precisemos de solicitações especiais de UAT para o teste de certificado da app store. | C |  |





## 3. Recursos da experiência de autenticação {#authn-exp-features}


| Não | Recurso | Descrição | Prioridade | Notas |
|-----|----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| 3.1 | Conversão de autenticação acima da expectativa mínima | O MVPD garante a taxa mínima de conversão para se provar funcional (5%) e razoável (30%). | A |  |
| 3.2 | Recuperação de senha em linha | O MVPD fornece um meio de recuperar senhas em linha para o fluxo do AuthN federado. | A |  |
| 3.3 | Registro de Conta Inline | O MVPD fornece um meio de criar uma nova conta em linha para o fluxo federado do AuthN. | A |  |
| 3.4 | Ajuda/suporte em linha | O MVPD fornece um meio de fornecer ajuda durante o fluxo do AuthN federado. | A |  |
| 3.5 | Autenticação interna baseada em modem | O MVPD autentica automaticamente um dispositivo quando ele está na rede local de um modelo registrado (somente ISP MVPD). | B | Essa é uma prioridade mais baixa porque é uma otimização que muitos ainda não podem apoiar e introduz alguns desafios para mitigação da fraude e controles dos pais |
Agora é possível importar o código da tabela do Markdown diretamente usando a caixa de diálogo Arquivo/Colar dados da tabela...



## 4. Recursos do Analytics {#analytics-features}


| Não | Recurso | Descrição | Prioridade |
|-----|--------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| 4.1 | Alinhamento do funil de conversão de autenticação | O MVPD tem uma métrica para solicitações AuthN que começa com a solicitação SAML AuthN - para alinhar-se às métricas de autenticação Primetime e de solicitação AuthN do Programador. | A |
| 4.2 | Usuários únicos | Usuários que foram autenticados com êxito e deduplicados em um rollup mensal ao longo dos dias. | A |
| 4.3 | Contabilização de Fuso Horário | Os relatórios incluem o fuso horário de quando o dia vira. | A |





## 5. Recursos da mitigação da fraude {#fraud-mitgn-features}


| Não | Recurso | Descrição | Prioridade | Notas |
|-----|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------|
| 5.1 | Validação do assinante de vídeo na autenticação | O MVPD garante que o usuário seja um assinante de vídeo válido durante o fluxo de AuthN. | A |  |
| 5.2 | Limite de taxa para autenticação/autorização | O MVPD suporta limitação em seus serviços da Web para limitar o uso de uma conta de usuário específica, quando apropriado. | B |  |
| 5.3 | UserID persistente com escopo global para Adobe | O MVPD garante que o Adobe tenha um UserID que possa ser rastreado em programadores para fraude. Isso não precisa ser fornecido diretamente ao cliente. | B | Especificação de OMAP (Online Multimedia Authorization Protocol, protocolo de autorização de multimídia online) e RUM (Real User Monitoring, monitoramento de usuário real). |
| 5.4 | Validação de uso simultâneo | O MVPD tem um meio de rastrear e limitar o uso simultâneo da conta de assinante além de um limite de negócios. | B |  |

## P1. Recursos funcionais específicos de proxy {#proxy-sp-func-features}

| Não | Descrição | Prioridade | Notas |
|-------|--------------------------------------------------------------------------------|----------|---------------------------------------------------|
| P 1.1 | Proxy responsável por manter a precisão da lista atualizada de subMVPDs | A |  |
| P 1.2 | O proxy fornece o logotipo de tamanho adequado para cada subMVPD | A | Alguns subMVPDs ao vivo não têm o tamanho correto do logotipo |
| P 1,3 | O proxy fornece a página de logon com a marca adequada para cada subMVPD | A |  |
| P 1,4 | Proxy responsável por direcionar marcas de provedores de serviços específicos com lista subMVPD | B |  |
| P 1,5 | O proxy especifica todas as propriedades do subMVPD corretamente (tamanho do iFrame, TTL, logotipo etc.) | A |  |
| P 1,6 | O proxy especifica entityID separada | B |  |

## P2. Recursos operacionais do proxy {#proxy-op-features}

| Não | Descrição | Prioridade |
|-------|----------------------------------------------------------------------------------------|----------|
| P 2.1 | A chave da API é segura | A |
| P 2.2 | Testar credenciais para o primeiro subMVPD usado na integração ao vivo para cada novo solicitante | A |
| P 2,3 | As listas do subMVPD são precisas e completas por solicitante | A |
