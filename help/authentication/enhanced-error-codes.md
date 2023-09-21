---
title: Códigos de erro aprimorados
description: Códigos de erro aprimorados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# Códigos de erro aprimorados {#enhanced-error-codes}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Visão geral {#overview}

Este documento descreve a lista de códigos de erro da API e informações adicionais sobre o erro retornadas aos aplicativos.

Para usar Códigos de erro aprimorados no aplicativo Programadores, é necessário fazer uma solicitação à equipe de suporte para habilitá-la com uma alteração de configuração.

## Tratamento de erro de resposta {#response-error-handling}

Na maioria dos cenários, a API de autenticação do Primetime inclui informações de erro adicionais no corpo da resposta para fornecer **contexto significativo** para explicar por que um determinado erro ocorreu e/ou possíveis soluções para corrigir automaticamente o problema.  *No entanto, em alguns casos específicos envolvendo fluxos de autenticação ou logout, os serviços de autenticação do Primetime podem retornar uma resposta de HTML ou um corpo vazio. Consulte a documentação da API para obter mais informações.*

Embora certos tipos de erros possam ser tratados automaticamente (como tentar novamente uma solicitação de autorização no caso de um tempo limite da rede ou exigir que o usuário se autentique novamente se a sessão expirar), outros tipos podem exigir alterações de configuração ou interação com a equipe de atendimento ao cliente. É importante para os programadores coletar e fornecer informações completas sobre os erros em tais casos.

A API de autenticação do Primetime retorna códigos de status HTTP no intervalo 400-500 para indicar falhas ou erros. Cada código de status HTTP tem determinadas implicações:

- Os códigos de erro 4xx implicam que o erro é gerado pelo cliente e que o cliente precisa fazer trabalho adicional para corrigi-lo (por exemplo, obter um token de acesso antes de chamar APIs protegidas ou fornecer qualquer parâmetro necessário)

- Os códigos de erro 5xx significam que o erro é gerado pelo servidor e que ele precisa fazer trabalho adicional para corrigi-lo.

As informações adicionais sobre o erro são incluídas no campo &quot;erro&quot; no corpo da resposta.




| Nome | Tipo | Exemplo | Descrição |
| --- | --- | --- | --- |
| **erro** | _objeto_ | JSON <br>    {<br>        &quot;Status&quot; : 403,<br>        &quot;code&quot; : &quot;network_connection_failure&quot;,<br>        &quot;message&quot; : &quot;Unable to contact your TV provider services&quot;,<br>        &quot;helpUrl&quot; : &quot;&quot;,<br>        &quot;trace&quot; : &quot;12f6fef9-d2e0-422b-a9d7-60d799abe353&quot;,<br>        &quot;action&quot; : &quot;retry&quot;<br>    }<br><br>—<br><br>XML<br><br>`<``error``>`<br><br>`<``status``>403</``status``>`<br><br>`<``code``>network_connection_failure</``code``>`<br><br>`<``message``>Unable to contact your TV provider services</``message``>   <``helpUrl``></``helpUrl``>`<br><br>`<``trace``>12f6fef9-d2e0-422b-a9d7-60d799abe353</``trace``>`<br><br>`<``action``>retry</``action``>`<br><br>`</``error``> ` | Uma coleção ou objetos de erro coletados ao tentar concluir a solicitação. |

</br>

As APIs do Adobe Primetime que lidam com vários itens (API de pré-autorização etc.) podem indicar que o processamento falhou para um item específico e foi bem-sucedido para outros itens usando informações de erro no nível do item. Neste caso, o ***&quot;erro&quot;*** objeto está localizado no nível do item e o corpo da resposta pode conter vários ***&quot;erros&quot;*** objetos - consulte a documentação da API.

</br>

| Exemplo com sucesso parcial e erro no nível do item |
| ---------------------- |
| <pre lang="json">JSON <br>{<br>  &quot;id&quot; : &quot;TestStream1&quot;,<br>  &quot;authorized&quot; : true <br>}, </br>{ </br>  &quot;id&quot; : &quot;TestStream2&quot;, <br>   &quot;authorized&quot; : false, </br>   &quot;erro&quot; : { <br> </br>      &quot;Status&quot; : 403,<br>      &quot;code&quot; : &quot;network_connection_failure&quot;,<br>      &quot;message&quot; : &quot;Unable to contact your TV provider services&quot;,<br>      &quot;detalhes&quot; : &quot;&quot;,<br>      &quot;helpUrl&quot; : &quot;&quot;,<br>      &quot;trace&quot; : &quot;8bcb17f9-b172-47d2-86d9-3eb146eba85e&quot;,<br>      &quot;action&quot; : &quot;retry&quot;</br>    }<br> </br>   }<br> ] </br>} </pre> |

</br>

Cada objeto de erro tem os seguintes parâmetros:

| Nome | Tipo | Exemplo | Restrito | Descrição |
|----|----|----|----|--------------|
| Status | *inteiro* | 403 | ♦ | O código de status HTTP de resposta conforme documentado na RFC 7231 (https://tools.ietf.org/html/rfc7231#section-6) <br> - 400 Solicitação incorreta <br> - 400 Solicitação incorreta <br> - 400 Solicitação incorreta <br> - 401 Não autorizado <br> - 403 Proibido <br> - 404 Não encontrado <br> - 405 Método não permitido <br> - Conflito 409 <br> - 410 Sumiu <br> - Falha na pré-condição 412 <br> - Muitas solicitações 429 <br> - Erro do servidor de intervalo 500 <br> - 503 Serviço indisponível |
| Código | *string* | network_connection_failure | ♦ | O código de erro de autenticação padrão do Primetime. A lista completa dos códigos de erro está incluída abaixo. |
| mensagem | *string* | Não é possível contatar os serviços do provedor de TV | | Mensagem legível por humanos que pode ser exibida ao usuário final. |
| detalhes | *string* | O pacote de assinatura não inclui o canal &quot;Live&quot; | | Em alguns casos, uma mensagem detalhada é fornecida pelos endpoints de autorização do MVPD ou pelo Programador através de regras de degradação. <br> <br> Observe que, se nenhuma mensagem personalizada tiver sido recebida dos serviços de parceiro, esse campo poderá não estar presente nos campos de erro. |
| helpUrl | *url* | &quot;&quot; | | Um URL que vincula mais informações sobre por que este erro ocorreu e possíveis soluções. <br> <br>  O URI representa um URL absoluto e não deve ser deduzido do código de erro. Dependendo do contexto de erro, um URL diferente pode ser fornecido. Por exemplo, o mesmo código de erro bad_request produzirá URLs diferentes para os serviços de autenticação e autorização. |
| trace | *string* | 12f6fef9-d2e0-422b-a9d7-60d799abe353 | | Um identificador exclusivo para essa resposta que pode ser usado ao entrar em contato com o suporte para identificar problemas específicos em cenários mais complexos. |
| ação | *string* | tentar novamente | ♦ | *Ação recomendada para corrigir a situação:* </br><br> -nenhum - Infelizmente, não há nenhuma ação predefinida para corrigir esse problema. Isso pode indicar uma invocação incorreta da API pública </br><br>-configuração - Uma alteração de configuração é necessária por meio do painel TVE ou entrando em contato com o suporte. </br><br>-application-registration - O aplicativo deve se registrar novamente. </br><br>-authentication - O usuário deve autenticar ou autenticar novamente. </br><br>-authorization - O usuário deve obter autorização para o recurso específico. </br><br>-degradação - Deve ser aplicada alguma forma de degradação. </br><br>-repetir - Tentar novamente a solicitação pode resolver o problema</br><br>-retry-after - Tentar novamente a solicitação após o período indicado pode resolver o problema. |

</br>

**Notas:**

- ***Restrito*** coluna *indica se o respectivo valor de campo representa um conjunto finito* (por exemplo, códigos de status HTTP existentes para &quot;*status*&quot;). Atualizações futuras dessa especificação poderão adicionar valores à lista restrita, mas não removerão nem alterarão as existentes. Campos irrestritos geralmente podem conter quaisquer dados, mas pode haver limitações em vigor para garantir um tamanho razoável.

- Cada resposta de Adobe conterá um &quot;Adobe-Request-Id&quot; que identifica a solicitação do cliente em todos os nossos serviços HTTP. O &quot;**trace** O campo &quot; complementa isso e eles devem ser relatados juntos.

## Códigos de status HTTP e códigos de erro {#http-status-codes-and-error-codes}

As inconsistências entre vários códigos de erro e seus códigos de status HTTP associados se devem aos requisitos de compatibilidade com versões anteriores de sdks e aplicativos mais antigos ( por exemplo, *unknown\_application* gera 400 solicitações incorretas enquanto *unknown\_software\_statement* 401 Não autorizado). A solução dessas inconsistências será direcionada em iterações futuras.

## Ações e códigos de erro {#actions-and-error-codes}

Para a maioria dos códigos de erro, várias ações podem ser qualificadas como caminhos para a correção do problema em andamento ou até mesmo várias ações podem ser necessárias para corrigi-las automaticamente. Optamos por indicar aquele com a maior probabilidade de correção do erro. A variável **ações** podem ser divididas em três categorias:

1. aqueles que tentam corrigir o contexto da solicitação (retry, retry-after)
1. aqueles que tentam corrigir o contexto de usuário no aplicativo (registro do aplicativo, autenticação, autorização)
1. aqueles que tentam corrigir o contexto de integração entre um aplicativo e um provedor de identidade (configuração, degradação)

Para a primeira categoria (repetir e repetir após), simplesmente repetir a mesma solicitação pode ser suficiente para resolver o problema. No caso de APIs que lidam com vários itens, o aplicativo deve repetir a solicitação e incluir apenas os itens com a ação &quot;repetir&quot; ou &quot;tentar depois&quot;. Para &quot;*tentar-depois* ação &quot;, uma &quot;<u>Repetir-após</u>O cabeçalho &quot; indicará quantos segundos o aplicativo deve aguardar antes de repetir a solicitação.

Para a 2ª e a 3ª categorias, a implementação da ação real é altamente dependente dos recursos do aplicativo. Por exemplo, &quot;*degradação*&quot; pode ser implementado como &quot;alternar para etapas temporárias de 15 minutos para permitir a reprodução do conteúdo pelos usuários&quot; ou como &quot;ferramenta automática para aplicar a degradação AUTHN-ALL ou AUTHZ-ALL para sua integração com o MVPD especificado&quot;. Semelhante a *autenticação*&quot;A ação do pode acionar uma autenticação passiva (autenticação de canal traseiro) em um tablet e um fluxo de autenticação de 2ª tela completo em TVs conectadas. É por isso que optamos por fornecer URLs completos com esquema e todos os parâmetros.

## Códigos de erro {#error-codes}

A tabela de erros abaixo lista os possíveis códigos de erro, mensagens associadas e possíveis ações.

| Ação | Código de erro | Código de status HTTP | Descrição |
|---|---|---|--------------|
| configuração | *authorization_denied_by_mvpd* | 403 | O MVPD retornou uma decisão de &quot;Negação&quot; ao solicitar autorização para o recurso especificado. |
|  | *authorization_denied_by_parent_controls* | 403 | O MVPD retornou uma decisão &quot;Negar&quot; devido às configurações de controles dos pais para o recurso especificado. |
|  | *authorization_denied_by_programmer* | 403 | A regra de degradação aplicada pelo Programador impõe uma decisão de &quot;Negação&quot; para o usuário atual. |
|  | *bad_request* | 400 | A solicitação de API é inválida ou está formada incorretamente. Consulte a documentação da API para determinar os requisitos da solicitação. |
|  | *individualization_service_unavailable* | 503 | A solicitação falhou devido ao serviço de individualização estar indisponível. |
|  | *internal_error* | 500 | A solicitação falhou devido a um erro interno do servidor. |
|  | *invalid_client_time* | 400 | A data/hora/fuso horário do computador cliente não está definida corretamente. Isso provavelmente levará a erros de autenticação/autorização. |
|  | *invalid_custom_scheme* | 400 | O esquema personalizado especificado usado no registro do aplicativo não é reconhecido. Verifique a configuração do painel TVE para obter os valores adequados do esquema personalizado. |
|  | *invalid_domain* | 400 | O solicitante está usando um domínio inválido. Todos os domínios usados por uma ID de solicitante específica precisam ser colocados na lista de permissões pelo Adobe. |
|  | *invalid_header* | 400 | A solicitação falhou porque continha um cabeçalho inválido. Consulte a documentação da API para determinar quais cabeçalhos são válidos para sua solicitação e se há limitações para o valor deles. |
|  | *invalid_http_method* | 405 | O método HTTP associado à solicitação não é compatível. Consulte a documentação da API para determinar os métodos HTTP compatíveis com sua solicitação. |
|  | *invalid_parameter_value* | 400 | A solicitação falhou porque continha um parâmetro ou valor de parâmetro inválido. Consulte a documentação da API para determinar quais parâmetros são válidos para sua solicitação e se há limitações para o valor deles. |
|  | *invalid_resource_value* | 400 | A solicitação falhou porque um recurso inválido ou malformado foi usado. Revise a documentação da API para determinar como os recursos complexos devem ser codificados para sua solicitação e se há limitações para seu valor e/ou tamanho. |
|  | *invalid_registration_code | 404 | O código de registro especificado não é mais válido ou expirou. |
|  | *invalid_service_configuration* | 500 | A solicitação falhou devido à configuração incorreta do serviço. |
|  | *missing_authentication_header* | 400 | A solicitação falhou porque não contém o cabeçalho de autenticação necessário para a API específica. |
|  | *missing_resource_mapping* | 400 | Não há mapeamento correspondente para o recurso especificado. Entre em contato com o suporte para corrigir o mapeamento necessário. |
|  | *preauthorization_denied_by_mvpd* | 403 | O MVPD retornou uma decisão de &quot;Negação&quot; ao solicitar pré-autorização para o recurso especificado. |
|  | *pré-autorização_negada_por_programador* | 403 | As regras de degradação aplicadas pelo Programador impõem uma decisão de &quot;Negação&quot; para o usuário atual. |
|  | *registration_code_service_unavailable* | 503 | A solicitação falhou porque o serviço de código de registro não está disponível. |
|  | *service_unavailable | 503 | A solicitação falhou devido ao fato de que o serviço de autenticação ou autorização não está disponível. |
|  | *access_token_unavailable* | 400 | A solicitação falhou devido a um erro inesperado ao recuperar o token de acesso. Verifique a configuração do painel TVE para obter instruções de software disponíveis e esquemas personalizados registrados. |
|  | *unsupported_client_version* | 400 | Esta versão do SDK de autenticação do Primetime é muito antiga e não é mais suportada. Consulte a documentação da API para conhecer as etapas necessárias para atualizar para a versão mais recente. |
|  | *network_required_ssl* | 403 | Há um problema de conexão SSL com o serviço de parceiro de destino. Contate a equipe de suporte. |
|  | *recursos_demais* | 403 | A solicitação de autorização ou pré-autorização falhou porque muitos recursos foram consultados. Entre em contato com a equipe de suporte para configurar corretamente as limitações de autorização e pré-autorização. |
|  | *programador_desconhecido | 400 | O programador ou provedor de serviços não é reconhecido. Use o Painel TVE para registrar o programador especificado. |
|  | *aplicativo_desconhecido* | 400 | O aplicativo não é reconhecido. Use o Painel TVE para registrar o aplicativo especificado. |
|  | *integração_desconhecida* | 400 | A integração entre o programador especificado e o provedor de identidade não existe. Use o painel TVE para criar a integração necessária. |
|  | *instrução_de_software_desconhecido* | 401 | A instrução de software associada ao token de acesso não é reconhecida. Entre em contato com a equipe de suporte para esclarecer o status da declaração do software. |
| registro de aplicativos | *access_token_expired* | 401 | O token de acesso expirou. O aplicativo deve atualizar o token de acesso conforme indicado na documentação da API. |
|  | *invalid_access_token_signature* | 401 | A assinatura do token de acesso não é mais válida. O aplicativo deve atualizar o token de acesso conforme indicado na documentação da API. |
|  | *invalid_client_id* | 401 | O identificador de cliente associado não é reconhecido. O aplicativo deve seguir o processo de registro conforme indicado na documentação da API. |
| autenticação | *authentication_session_expired* | 410 | A sessão de autenticação atual expirou. O usuário deve autenticar novamente com um MVPD compatível para continuar. |
|  | *authentication_session_missing* | 401 | Não foi possível recuperar a sessão de autenticação associada a esta solicitação. O usuário deve autenticar novamente com um MVPD compatível para continuar. |
|  | *authentication_session_invalidated* | 401 | A sessão de autenticação foi invalidada pelo provedor de identidade. O usuário deve autenticar novamente com um MVPD compatível para continuar. |
|  | *authentication_session_issuer_mismatch | 400 | A solicitação de autorização falhou devido ao fato de que o MVPD indicado para o fluxo de autorização é diferente daquele que emitiu a sessão de autenticação. O usuário deve autenticar novamente com o MVPD desejado para continuar. |
|  | *authorization_denied_by_hba_policies* | 403 | O MVPD retornou uma decisão de &quot;Negação&quot; devido a políticas de autenticação doméstica. A autenticação atual foi obtida usando um HBA (fluxo de autenticação baseado em início), mas o dispositivo não está mais em casa ao solicitar autorização para o recurso especificado. O usuário deve autenticar novamente com um MVPD compatível para continuar. |
|  | *identity_not_known_by_mvpd* | 403 | A solicitação de autorização falhou devido ao fato de que a identidade do usuário não foi reconhecida pelo MVPD. |
| autorização | *authorization_expired* | 410 | A autorização anterior do recurso especificado expirou. O usuário deve obter uma nova autorização para continuar. |
|  | *authorization_not_found* | 404 | Nenhuma autorização foi encontrada para o recurso especificado. O usuário deve obter uma nova autorização para continuar. |
|  | *device_identifier_mismatch* | 403 | O identificador de dispositivo especificado não corresponde à identificação do dispositivo de autorização. O usuário deve obter uma nova autorização para continuar. |
| tentar novamente | **network_connection_failure** | 403 | Falha de conexão com o serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema. |
|  | *network_connection_timeout* | 403 | Houve um tempo limite de conexão com o serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema. |
|  | *network_received_error* | 403 | Erro de leitura ao recuperar a resposta do serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema. |
|  | *maximum_execution_time_aded* | 403 | A solicitação não foi concluída no tempo máximo permitido. Tentar novamente a solicitação pode resolver o problema. |
| tentar-depois | *muitas_solicitações* | 429 | Muitas solicitações foram enviadas em um determinado intervalo. O aplicativo pode repetir a solicitação após o período sugerido. |
|  | *user_rate_limit_aded* | 429 | Muitas solicitações foram emitidas por um usuário específico em um determinado intervalo. O aplicativo pode repetir a solicitação após o período sugerido. |
