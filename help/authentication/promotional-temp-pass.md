---
title: Aprovação temporária promocional
description: Aprovação temporária promocional
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 0%

---


# Aprovação temporária promocional {#promotional-temp-pass}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Resumo dos recursos {#feature-summary}

O Portal Promocional permite que os Programadores ofereçam acesso temporário ao seu conteúdo protegido para usuários que não têm credenciais de conta com um MVPD.

O Portal Promocional foi projetado para ser usado na execução de campanhas promocionais, onde o usuário, após fornecer informações de identificação válidas (por exemplo, endereço de email) ao Programador, poderá consumir um **número predefinido de títulos VOD diferentes para um período predefinido**.

>[!IMPORTANT]
>
>O Adobe não armazena informações pessoais identificáveis (PII). Portanto, o Programador deve definir um hash sobre as informações fornecidas pelo usuário exclusivo sobre as APIs de autenticação do Primetime.

O Fluxo de Temp Promocional é criado sobre o [Aprovação temporária](/help/authentication/temp-pass.md) , o que significa que inclui todas as funcionalidades de aprovação temporária.

Quando o número máximo predefinido de títulos de VOD ou o período predefinido for excedido, esse usuário não poderá acessar o conteúdo no mesmo dispositivo ou usando as mesmas informações de identificador de usuário (por exemplo, endereço de email) até que os tokens de autorização sejam apagados do servidor de autenticação da Adobe Primetime.

>[!NOTE]
>
>O Temp Pass faz parte do pacote Premium Workflow . Entre em contato com seu representante de vendas do Primetime, caso esteja interessado em usar essa funcionalidade.

## Comparação de passagem temporária e promoção de aprovação temporária {#tp-ptp-comparison}

| Aprovação temporária | Aprovação temporária promocional |
|----------------------------------|----------------------------------------------------------------------------------------|
| Acesso ao conteúdo <ul><li>baseado no tempo</li></ul> | Acesso ao conteúdo <ul><li>baseado no tempo</li><li>com base no número de recursos</li></ul> |
| Acessar a segurança com base em <ul><li>ID do dispositivo</li></ul> | Segurança com base em <ul><li>ID do dispositivo</li><li>hash sobre informações de identificador de usuário fornecidas (por exemplo, email)</li></ul> |
| API de erro do cliente disponível | API de erro do cliente disponível |
| Redefinição/limpeza disponível | Redefinição/limpeza disponível |

## Detalhes do recurso {#feature-details}

Esse recurso permite que os usuários acessem conteúdo promocional de um dispositivo específico (telefone e tablet) após fornecer informações exclusivas, como o endereço de email, no aplicativo do Programador.

O Programador fornecerá um hash sobre a PII do usuário nas APIs de autenticação e autorização. Esse hash será usado junto com a ID do dispositivo na geração de uma chave exclusiva para identificar o usuário e o dispositivo.

Com base na ID do dispositivo e nas informações fornecidas pelo usuário e seguindo a lógica abaixo, a autenticação da Adobe Primetime determinará se o usuário está em uma nova versão de avaliação ou em uma existente:

* novo hash sobre informações fornecidas pelo usuário (por exemplo, email), nova ID do dispositivo => nova avaliação
* hash existente sobre informações fornecidas pelo usuário (por exemplo, email), nova ID do dispositivo => avaliação existente (com hash sobre informações fornecidas pelo usuário (por exemplo, email))
* novo hash sobre informações fornecidas pelo usuário (por exemplo, email), ID do dispositivo existente => avaliação existente (com ID do dispositivo existente)
* hash existente sobre informações fornecidas pelo usuário (por exemplo, email), ID do dispositivo existente => avaliação existente

>[!NOTE]
>A validação e o hash das informações fornecidas pelo usuário são manipulados pelo Programador, não pelo Adobe.

**O recurso de Aprovação de Temp Promocional pode ser configurado com base nas seguintes propriedades:**

* Chave de informações fornecida pelo usuário (por exemplo, email)
* Número de recursos que o usuário tem direito a consumir
* TTL - o período em que o usuário tem direito a consumir o número configurado de recursos

### Metadados do usuário {#user-metadata}

Para facilitar a execução da aplicação do programador, **informações de metadados do usuário são expostas** no Percurso de Temp Promocional, com as chaves correspondentes (para ativar as chaves, entre em contato com tve-support@adobe.com):

* **remain_resources**: o número de recursos restantes que o usuário atual tem direito a consumir
* **used_assets**: a lista de recursos que o usuário atual já consumiu
* **expiration_date**: a data de expiração do usuário atual

### Como o tempo de visualização é calculado? {#compute-viewing-time}

O tempo em que uma passagem temporária permanece válida não está correlacionado ao tempo em que um usuário gasta visualizando o conteúdo no aplicativo do Programador. Após a solicitação inicial do usuário para autorização por meio do Tempo de expiração promocional, calcula-se um tempo de expiração adicionando o tempo de solicitação atual inicial ao TTL (período de duração) especificado pelo Programador.

### Autenticação e autorização {#authn-authz}

Para fluxos de mensagens promocionais de aprovação temporária, a autenticação e a autorização não se comunicam com um MVPD real, **assim, todas as solicitações de autorização terão êxito** desde que todas estas condições sejam cumpridas:

* os tokens de autorização são válidos para recursos especificados
* número de **used_assets** é inferior ao limite definido pelo Programador
* **expiration_date** é após a data atual.

### Comportamento de comprovação {#preflight-beh}

Quando uma solicitação de comprovação ou pré-autorização é feita para um MVPD de Aprovação de Modelo Promocional, a resposta de Comprovação correspondente retornada conterá toda a lista de recursos da Solicitação de Comprovação como comprovação bem-sucedida.

A lógica por trás disso é: as condições de autorização do Pass Promocional de Temp se baseiam no limite de tempo e número de recursos, e não em recursos específicos. Mais especificamente, desde que a restrição de tempo seja atendida e desde que o limite de recursos não seja excedido, os recursos chamados serão autorizados.

### SSO {#sso}

O SSO não está ativado para instâncias de Aprovação de Temp Promocional, que é configurada com &quot;Autenticação por Solicitante&quot; ativada. Isso significa que, quando o usuário alternar do aplicativo A para outro aplicativo B, ambos integrados com o mesmo Passe Temp Promocional, o usuário não será conectado automaticamente.

### Logout {#logout}

Todos os tokens em um dispositivo são excluídos no logout. Portanto, a alternância do Relatório de Temp Promocional para um MVPD selecionado pelo usuário não deve depender dessa implementação. A recomendação é usar a variável `setSelectedProvider(null)` para limpar o estado do aplicativo e reiniciar o fluxo de autenticação, que tem uma melhor experiência do usuário.

### Diagrama de fluxo de aprovação temporária promocional {#promo-tempass-flowdia}

![Diagrama de fluxo de aprovação temporária promocional](assets/promo-temp-pass-flow.png)

*Figura: Fluxo de aprovação temporária promocional*

## Implementar o fluxo temporário promocional {#impl-promo-tempass}

O Fluxo de Temp Promocional exige as seguintes funcionalidades do lado do cliente:

* **Informações do identificador do usuário, por exemplo propagação de endereço de email** (enviando o endereço de email do usuário nos fluxos de autenticação e autorização). O e-mail é exigido pela autenticação da Adobe Primetime para vincular os tokens de autenticação e autorização (semelhante ao caso da variável `device_ID`, obrigatório em todas as chamadas).
* **Forçar autenticação** - permitindo que o Programador force um fluxo de autenticação quando o usuário já estiver autenticado. Essa funcionalidade é necessária para forçar uma atualização dos metadados do usuário (a chave de metadados do usuário) **used_assets** contém o número de recursos disponíveis) sempre que o aplicativo é iniciado. Como o usuário pode fazer logon em vários dispositivos, os metadados do usuário presentes no dispositivo durante a inicialização do aplicativo não são confiáveis e precisamos atualizá-los para refletir o estado atual desse usuário específico (identificado pelo endereço de email).


>[!IMPORTANT]
>A autenticação forçada é possível somente no iOS e Android.
>A autenticação do Primetime não tem um mecanismo integrado para interromper o streaming gratuito após X minutos terem passado. A autenticação do Primetime deixará de emitir **autorização** e **mídia curta** tokens assim que o usuário consome os recursos livres de Y. Cabe aos programadores restringir o acesso assim que a Aprovação de modelo promocional expirar.

## Segurança {#security}

>[!IMPORTANT]
>O Adobe não armazena informações pessoais identificáveis (PII). Portanto, o Programador deve definir um hash sobre as informações fornecidas pelo usuário exclusivo sobre as APIs de autenticação do Primetime.

**Hash das informações do identificador de usuário**

O Adobe recomenda usar a variável **SHA-2** família ou **SHA-256**, **SHA-512** nos dados antes de serem enviados para o Adobe.

Por exemplo, **SHA-256** over **&quot;user@domain.com&quot;** é **&quot;f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&quot;**.

## Redefinir ou remover aprovação temporária promocional {#reset-promo-tempass}

Determinadas regras de negócios exigem uma limpeza regular de Aprovação de Temp Promocional. Para fazer isso, a autenticação do Primetime fornece aos programadores uma *público* API da Web, descrita abaixo:

| `DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset` |
|----|
| <ul><li>Protocolo: **https**</li><li>Host:<ul><li>Versão: **mgmt.auth.adobe.com**</li><li>Prequal: **mgmt-prequal.auth.adobe.com**</li></ul></li><li>Caminho: **/reset-tempass/v2/reset**</li><li>Parâmetros de consulta: **device_id=all&amp;requestor_id=THE_REQUESTOR_ID&amp;mvpd_id=THE_TEMPASS_MVPD_ID**</li><li>cabeçalhos: ApiKey: **1232293681726481**</li> <li>Resposta:<ul><li>Sucesso: **HTTP 204**</li><li>Falha: **HTTP 400** para pedidos incorretos, **HTTP 401** se ApiKey não especificado, **HTTP 403** se ApiKey for inválido</li></ul></li></ul> |

Além dos requisitos para limpar o Temp Pass, o Promotional Temp Pass usa o hash sobre as informações do identificador de usuário enviadas como **generic_data** na autenticação e autorização para limpeza.

O hash será enviado, não para o JSON inteiro:

```cURL
$ curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=FlexibleTempPass"
```

### Clientes compatíveis {#supported-clients}

| Clientes de autenticação da Adobe Primetime | Aprovação temporária promocional | Ferramenta Redefinir | Suporta Código de Resposta Dedicado / Erro do Cliente |
|:--------------------------------------:|:---------------------:|:----------:|:-----------------------------------------------:|
| Ativador de acesso JS | SIM | SIM | SIM (a partir da v 3.0.0) |
| iOS cliente nativo | SIM | SIM | SIM (a partir da v 1.10) |
| Android de cliente nativo | SIM | SIM | SIM |
| API sem cliente | SIM | SIM | NÃO |


## Limitações {#limitations}

Esta seção descreve as limitações que se aplicam à implementação atual do Passe de Temp Promocional.

### Clientless {#lim-clientless}

**Dispositivos inteligentes sem uma ID de dispositivo exclusiva**

Nem todos os aplicativos de dispositivos inteligentes podem fornecer uma ID de dispositivo exclusiva. Na ausência de um, a autenticação da Adobe Primetime pode usar a UUID gerada pelo Adobe Registration Code Service como a ID de dispositivo exclusiva. Isso significa que quando o usuário sair, os tokens de autenticação e autorização serão excluídos. Depois que o usuário tentar autenticar novamente, desta vez com informações do usuário diferentes (por exemplo, email), ele poderá autorizar novamente. O Adobe recomenda adicionar um fluxo de interface que não permitirá que um usuário &quot;engane&quot; o sistema e adicione lógica para determinar se é um novo usuário que solicita uma avaliação ou uma avaliação existente.

**Redefinir / limpar aprovação temporária**

A mensagem Reset Temp Pass for Clientless não está disponível nos casos específicos de Xbox360 e Xbox One, pois essas plataformas exigem uma análise de ID de dispositivo adicional, o que não é possível na ferramenta Reset Temp Pass.

<!--
>[!RELATEDINFORMATION]
>
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
-->