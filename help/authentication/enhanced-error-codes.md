---
title: Códigos de erro aprimorados
description: Códigos de erro aprimorados
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# Códigos de erro aprimorados {#enhanced-error-codes}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview}

Este documento descreve a lista de códigos de erro de API e informações de erro adicionais retornadas aos aplicativos.

Para usar Códigos de erro aprimorados no aplicativo Programadores, é necessário fazer uma solicitação para a equipe de Suporte para habilitá-la com uma alteração de configuração.

## Tratamento de erros de resposta {#response-error-handling}

Na maioria dos cenários, a API de autenticação do Primetime inclui informações de erro adicionais no corpo da resposta para fornecer **contexto significativo** para o motivo pelo qual um determinado erro ocorreu e/ou possíveis soluções para corrigir o problema automaticamente.  *No entanto, em alguns casos específicos envolvendo fluxos de autenticação ou de logout, os serviços de Autenticação do Primetime podem retornar uma resposta de HTML ou um corpo vazio - verifique a documentação da API para obter mais informações.*

Embora certos tipos de erros possam ser tratados automaticamente (como tentar novamente uma solicitação de autorização em caso de tempo limite de rede ou exigir que o usuário se autentique novamente se a sessão tiver expirado), outros tipos podem exigir alterações na configuração ou interação com o atendimento ao cliente. É importante que os programadores coletem e forneçam informações completas sobre os erros nesses casos.

A API de autenticação do Primetime retorna códigos de status HTTP no intervalo 400-500 para indicar falhas ou erros. Cada código de status HTTP tem certas implicações:

- Os códigos de erro 4xx implicam que o erro é gerado pelo cliente e que o cliente precisa fazer trabalho adicional para corrigi-lo (por exemplo, obter um token de acesso antes de invocar APIs protegidas ou fornecer qualquer parâmetro necessário)

- Os códigos de erro 5xx implicam que o erro é gerado pelo servidor e que o servidor precisa fazer trabalho adicional para corrigi-lo.

As informações adicionais sobre o erro são incluídas no campo &quot;erro&quot; no corpo da resposta. 




| Nome | Tipo | Exemplo | Descrição |
| --- | --- | --- | --- |
| **erro** | _objeto_ | JSON <br>    {<br>        &quot;status&quot; : 403,<br>        &quot;code&quot; : &quot;network_connection_failure&quot;,<br>        &quot;message&quot; : &quot;Não é possível entrar em contato com os serviços do provedor de TV&quot;,<br>        &quot;helpUrl&quot; : &quot;&quot;,<br>        &quot;trace&quot; : &quot;12f6fef9-d2e0-422b-a9d7-60d799abe353&quot;,<br>        &quot;Ação&quot; : &quot;repetir&quot;<br>    }<br><br>—<br><br>XML<br><br>`<``error``>`<br><br>`<``status``>403</``status``>`<br><br>`<``code``>network_connection_failure</``code``>`<br><br>`<``message``>Unable to contact your TV provider services</``message``>   <``helpUrl``></``helpUrl``>`<br><br>`<``trace``>12f6fef9-d2e0-422b-a9d7-60d799abe353</``trace``>`<br><br>`<``action``>retry</``action``>`<br><br>`</``error``> ` | Uma coleção ou objetos de erro coletados ao tentar concluir a solicitação. |

</br>

As APIs do Adobe Primetime que lidam com vários itens (API de pré-autorização etc.) podem indicar se o processamento falhou para um item específico e foi bem-sucedido para outros itens usando informações de erro no nível do item. Nesse caso, a variável ***&quot;error&quot;*** O objeto está localizado no nível do item e o corpo da resposta pode conter vários ***&quot;errors&quot;*** objetos - consulte a documentação da API.

</br>

| Exemplo com sucesso parcial e erro no nível do item |
| ---------------------- |
| <pre lang="json">JSON <br>{<br>  &quot;id&quot; : &quot;TestStream1&quot;,<br>  &quot;Autorizado&quot; : true <br>}, </br>{ </br>  &quot;id&quot; : &quot;TestStream2&quot;, <br>   &quot;Autorizado&quot; : false, </br>   &quot;error&quot; : { <br> </br>      &quot;status&quot; : 403,<br>      &quot;code&quot; : &quot;network_connection_failure&quot;,<br>      &quot;message&quot; : &quot;Não é possível entrar em contato com os serviços do provedor de TV&quot;,<br>      &quot;detalhes&quot; : &quot;&quot;,<br>      &quot;helpUrl&quot; : &quot;&quot;,<br>      &quot;trace&quot; : &quot;8bcb17f9-b172-47d2-86d9-3eb146eba85e&quot;,<br>      &quot;Ação&quot; : &quot;repetir&quot;</br>    }<br> </br>   }<br> ] </br>} </pre> |

</br>

Cada objeto de erro tem os seguintes parâmetros:

| Nome | Tipo | Exemplo | Restrito | Descrição |
|----|----|----|----|--------------|
| Status | *integer* | 403 | ♦ | O código de status HTTP de resposta conforme documentado no RFC 7231 (https://tools.ietf.org/html/rfc7231#section-6) <br> - 400 Solicitação inválida <br> - 400 Solicitação inválida <br> - 400 Solicitação inválida <br> - 401 Não Autorizado <br> - 403 Proibido <br> - 404 Não encontrado <br> - Método 405 não permitido <br> - Conflito 409 <br> - 410 Ausência <br> - Falha na pré-condição 412 <br> - 429 Demasiados pedidos <br> - Erro do servidor de intervalo 500 <br> - 503 Serviço indisponível |
| Código | *string* | network_connection_failure | ♦ | O código de erro padrão de autenticação do Primetime. A lista completa de códigos de erro está incluída abaixo. |
| message | *string* | Não é possível entrar em contato com os serviços do provedor de TV |  | Mensagem legível por humano que pode ser exibida para o usuário final. |
| detalhes | *string* | Seu pacote de assinatura não inclui o canal &quot;Ao vivo&quot; |  | Em alguns casos, uma mensagem detalhada é fornecida pelos endpoints de autorização do MVPD ou pelo Programador por meio de regras de degradação. <br> <br> Observe que se nenhuma mensagem personalizada foi recebida dos serviços do parceiro, esse campo pode não estar presente nos campos de erro. |
| helpUrl | *url* | &quot;&quot; |  | Um URL que oferece um link para obter mais informações sobre por que esse erro ocorreu e possíveis soluções. <br> <br>  O URI representa um URL absoluto e não deve ser inferido do código de erro. Dependendo do contexto de erro, um url diferente pode ser fornecido. Por exemplo, o mesmo código de erro bad_request produzirá urls diferentes para serviços de autenticação e autorização. |
| traçar | *string* | 12f6fef9-d2e0-422b-a9d7-60d799abe353 |  | Um identificador exclusivo para essa resposta que pode ser usado ao entrar em contato com o suporte para identificar problemas específicos em cenários mais complexos. |
| ação | *string* | tentar novamente | ♦ | *Ação recomendada para remediar a situação:* </br><br> -none - Infelizmente não há nenhuma ação predefinida para corrigir esse problema. Isso pode indicar uma invocação incorreta da API pública </br><br>-configuration - Uma alteração da configuração é necessária por meio do painel TVE ou entrando em contato com o suporte. </br><br>-application-registration - O pedido deve registrar-se novamente. </br><br>-authentication - O usuário deve autenticar ou autenticar novamente. </br><br>-authorization - O usuário deve obter autorização para o recurso específico. </br><br>-degradação - Deve ser aplicada alguma forma de degradação. </br><br>-retry - Tentar novamente a solicitação pode resolver o problema</br><br>-retry-after - Tentar novamente a solicitação após o período de tempo indicado pode resolver o problema. |

</br>

**Notas:**

- ***Restrito*** column *indica se o respectivo valor de campo representa um conjunto finito* (por exemplo, códigos de status HTTP existentes para &quot;*status*&quot;). Atualizações futuras a essa especificação podem adicionar valores à lista restrita, mas não removerão nem alterarão os existentes. Campos irrestritos geralmente podem conter quaisquer dados, mas pode haver limitações para garantir um tamanho razoável.

- Cada resposta do Adobe conterá um &quot;Adobe-Request-Id&quot; que identifica a solicitação do cliente em todos os nossos serviços HTTP. O &quot;**traçar**&quot; complementa isso e devem ser reportados juntos. 

## Códigos de status HTTP e códigos de erro {#http-status-codes-and-error-codes}

As inconsistências entre vários códigos de erro e seus códigos de status HTTP associados são devidas devido aos requisitos de compatibilidade com versões anteriores com sdks e aplicativos mais antigos ( por exemplo *unknown\_application* gera 400 Solicitação inválida enquanto *unknown\_software\_statement* 401 Não autorizado). Resolver essas inconsistências será direcionado em iterações futuras. 
 
## Ações e códigos de erro {#actions-and-error-codes}

Para a maioria dos códigos de erro, várias ações podem ser qualificadas como caminhos para corrigir o problema em mãos ou até mesmo várias ações podem ser necessárias para corrigi-las automaticamente. Optamos por indicar aquele com a maior probabilidade para corrigir o erro. O **ações** pode ser dividido em três categorias:

1. aqueles que tentam corrigir o contexto da solicitação (tentar novamente, tentar depois) 
1. aqueles que tentam corrigir o contexto do usuário no aplicativo (registro do pedido, autenticação, autorização) 
1. aqueles que tentam corrigir o contexto de integração entre um aplicativo e um provedor de identidade (configuração, degradação)

Para a primeira categoria (tentativa e tentativa após), simplesmente tentar novamente a mesma solicitação pode ser suficiente para resolver o problema. Nos casos de APIs que lidam com vários itens, o aplicativo deve repetir a solicitação e incluir apenas os itens com a ação &quot;tentar novamente&quot; ou &quot;tentar depois&quot;. Para &quot;*repetir depois*&quot; ação, um &quot;<u>Repetir após</u>&quot; indicará quantos segundos o aplicativo deve aguardar antes de repetir a solicitação.

Para a segunda e a terceira categoria, a implementação da ação real é altamente dependente dos recursos do aplicativo. Por exemplo, &quot;*degradação*&quot; pode ser implementado como &quot;alternar para 15 minutos de passagens temporárias para permitir que os usuários reproduzam o conteúdo&quot; ou como &quot;ferramenta automática para aplicar a degradação de AUTHN-ALL ou AUTHZ-ALL para sua integração com o MVPD especificado&quot;. Semelhante a um &quot;*autenticação*&quot; pode acionar uma autenticação passiva (autenticação de canal traseiro) em um tablet e um fluxo de autenticação de segunda tela completo em TVs conectadas. Foi por isso que optamos por fornecer URLs completos com esquema e todos os parâmetros. 

## Códigos de erro {#error-codes}

A tabela de erros abaixo lista os possíveis códigos de erro, mensagens associadas e ações possíveis.

| Ação | Código de erro | Código de status HTTP | Descrição |
|---|---|---|--------------|
| configuração | *authorization_denied_by_mvpd* | 403 | O MVPD retornou uma decisão de &quot;Negar&quot; ao solicitar autorização para o recurso especificado. |
|  | *authorization_denied_by_parental_controls* | 403 | O MVPD retornou uma decisão de &quot;negar&quot; devido às configurações de controles dos pais para o recurso especificado. |
|  | *authorization_denied_by_programmer* | 403 | A regra de degradação aplicada pelo Programador impõe uma decisão de &quot;Negar&quot; para o usuário atual. |
|  | *bad_request* | 400 | A solicitação da API é inválida ou foi formada incorretamente. Revise a documentação da API para determinar os requisitos da solicitação. |
|  | *individualization_service_unavailable* | 503 | A solicitação falhou porque o serviço de individualização não estava disponível. |
|  | *internal_error* | 500 | A solicitação falhou devido a um erro de servidor interno. |
|  | *invalid_client_time* | 400 | A data/hora/fuso horário da máquina cliente não está definida corretamente. Isso provavelmente levará a erros de autenticação/autorização. |
|  | *invalid_custom_scheme* | 400 | O esquema personalizado especificado utilizado no registro do pedido não é reconhecido. Verifique a configuração do painel TVE para obter os valores de esquema personalizados adequados. |
|  | *invalid_domain* | 400 | O solicitante está usando um domínio inválido. Todos os domínios usados por uma ID de solicitante específica precisam estar na lista de permissões do Adobe. |
|  | *invalid_header* | 400 | A solicitação falhou porque continha um cabeçalho inválido. Revise a documentação da API para determinar quais cabeçalhos são válidos para sua solicitação e se há limitações para seu valor. |
|  | *invalid_http_method* | 405 | Não há suporte para o método HTTP associado à solicitação. Revise a documentação da API para determinar os métodos HTTP compatíveis com sua solicitação. |
|  | *invalid_parameter_value* | 400 | A solicitação falhou porque continha um parâmetro ou valor de parâmetro inválido. Revise a documentação da API para determinar quais parâmetros são válidos para sua solicitação e se há limitações para seu valor. |
|  | *invalid_resource_value* | 400 | A solicitação falhou porque um recurso inválido ou malformado foi usado. Revise a documentação da API para determinar como os recursos complexos devem ser codificados para sua solicitação e se há limitações para seu valor e/ou tamanho. |
|  | *invalid_registration_code | 404 | O código de registro especificado não é mais válido ou expirou. |
|  | *invalid_service_configuration* | 500 | A solicitação falhou devido à configuração incorreta do serviço. |
|  | *missing_authentication_header* | 400 | A solicitação falhou porque não contém o cabeçalho de autenticação necessário para a API específica. |
|  | *missing_resource_mapping* | 400 | Não há mapeamento correspondente para o recurso especificado. Entre em contato com o suporte para corrigir o mapeamento necessário. |
|  | *preauthorization_denied_by_mvpd* | 403 | O MVPD retornou uma decisão de &quot;Negar&quot; ao solicitar pré-autorização para o recurso especificado. |
|  | *preauthorization_denied_by_programmer* | 403 | As regras de degradação aplicadas pelo Programador impõem uma decisão de &quot;Negar&quot; para o usuário atual. |
|  | *registration_code_service_unavailable* | 503 | A solicitação falhou porque o serviço de código de registro não está disponível. |
|  | *service_unavailable | 503 | A solicitação falhou porque o serviço de autenticação ou autorização não está disponível. |
|  | *access_token_unavailable* | 400 | A solicitação falhou devido a um erro inesperado ao recuperar o token de acesso. Verifique a configuração do painel TVE para ver as declarações de software disponíveis e os esquemas personalizados registrados. |
|  | *unsupported_client_version* | 400 | Esta versão do SDK de autenticação do Primetime é muito antiga e não é mais compatível. Verifique a documentação da API para ver as etapas necessárias para atualizar para a versão mais recente. |
|  | *network_required_ssl* | 403 | Há um problema de conexão SSL para o serviço de parceiro de destino. Entre em contato com a equipe de suporte. |
|  | *too_many_resources* | 403 | A solicitação de autorização ou pré-autorização falhou porque muitos recursos foram consultados. Entre em contato com a equipe de suporte para configurar corretamente as limitações de autorização e pré-autorização. |
|  | *unknown_programmer | 400 | O programador ou o provedor de serviços não é reconhecido. Use o painel TVE para registrar o programador especificado. |
|  | *unknown_application* | 400 | O aplicativo não é reconhecido. Use o painel TVE para registrar o aplicativo especificado. |
|  | *unknown_integration* | 400 | A integração entre o programador especificado e o provedor de identidade não existe. Use o painel TVE para criar a integração necessária. |
|  | *unknown_software_statement* | 401 | A declaração de software associada ao token de acesso não é reconhecida. Entre em contato com a equipe de suporte para esclarecer o status da declaração de software. |
| registro do pedido | *access_token_expirado* | 401 | O token de acesso expirou. O aplicativo deve atualizar o token de acesso, conforme indicado na documentação da API. |
|  | *invalid_access_token_signature* | 401 | A assinatura do token de acesso não é mais válida. O aplicativo deve atualizar o token de acesso, conforme indicado na documentação da API. |
|  | *invalid_client_id* | 401 | O identificador de cliente associado não é reconhecido. O aplicativo deve seguir o processo de registro do aplicativo, conforme indicado na documentação da API. |
| autenticação | *authentication_session_expires* | 410 | A sessão de autenticação atual expirou. O usuário deve autenticar novamente com um MVPD suportado para continuar. |
|  | *authentication_session_missing* | 401 | Não foi possível recuperar a sessão de autenticação associada a esta solicitação. O usuário deve autenticar novamente com um MVPD suportado para continuar. |
|  | *authentication_session_invalidated* | 401 | A sessão de autenticação foi invalidada pelo provedor de identidade. O usuário deve autenticar novamente com um MVPD suportado para continuar. |
|  | *authentication_session_issuers_mismatch | 400 | O pedido de autorização falhou devido ao fato de o MVPD indicado para o fluxo de autorização ser diferente daquele que emitiu a sessão de autenticação. O usuário deve autenticar novamente com o MVPD desejado para continuar. |
|  | *authorization_denied_by_hba_policies* | 403 | O MVPD retornou uma decisão de &quot;negar&quot; devido às políticas de autenticação baseadas em casa. A autenticação atual foi obtida usando um HBA (home-based authentication flow, fluxo de autenticação baseado em casa), mas o dispositivo não está mais em casa ao solicitar autorização para o recurso especificado. O usuário deve autenticar novamente com um MVPD suportado para continuar. |
|  | *identity_not_authorized_by_mvpd* | 403 | O pedido de autorização falhou devido ao fato de a identidade do utilizador não ter sido reconhecida pelo MVPD. |
| autorização | *authorization_expirado* | 410 | A autorização anterior para o recurso especificado expirou. O usuário deve obter uma nova autorização para continuar. |
|  | *authorization_not_found* | 404 | Não foi encontrada nenhuma autorização para o recurso especificado. O usuário deve obter uma nova autorização para continuar. |
|  | *device_identifier_mismatch* | 403 | O identificador de dispositivo especificado não corresponde à identificação do dispositivo de autorização. O usuário deve obter uma nova autorização para continuar. |
| tentar novamente | **network_connection_failure** | 403 | Houve uma falha de conexão com o serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema. |
|  | *network_connection_timeout* | 403 | Havia um tempo limite de conexão com o serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema. |
|  | *network_receive_error* | 403 | Erro de leitura ao recuperar a resposta do serviço de parceiro associado. Tentar novamente a solicitação pode resolver o problema. |
|  | *maximum_execution_time_aded* | 403 | A solicitação não foi concluída no tempo máximo permitido. Tentar novamente a solicitação pode resolver o problema. |
| repetir depois | *too_many_requests* | 429 | Muitas solicitações foram enviadas em um determinado intervalo. O aplicativo pode repetir a solicitação após o período sugerido. |
|  | *user_rate_limit_aded* | 429 | Muitas solicitações foram emitidas por um usuário específico em um intervalo específico. O aplicativo pode repetir a solicitação após o período sugerido. |

