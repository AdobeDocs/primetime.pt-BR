---
title: Autorização de MVPD
description: Autorização de MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Autorização de MVPD

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#mvpd-authz-overview}

A autorização (AuthZ) é executada por meio de comunicações de canal traseiro (servidor para servidor) entre um servidor de back-end hospedado pelo Adobe e o terminal MVPD AuthZ.

Para solicitações AuthZ, o endpoint de autorização deve ser capaz de processar pelo menos os seguintes parâmetros:

* **Uid**. A ID de usuário recebida da etapa de autenticação.

* **ID do recurso**. Uma string que identifica um determinado recurso de conteúdo. Essa ID de recurso é especificada pelo Programador e o MVPD deve reforçar as regras de negócios nesses recursos (por exemplo, verificando se o usuário está inscrito em um determinado canal).

Além de determinar se o usuário está autorizado, a resposta deve incluir o TTL (time-to-live) dessa autorização, ou seja, quando a autorização expira. Se o TTL não estiver definido, a solicitação AuthZ falhará.  Por isso, **o TTL é uma configuração obrigatória no lado da autenticação do Adobe Primetime**, a fim de cobrir o caso em que um MVPD não inclui o TTL no seu pedido.

## A Solicitação de Autorização {#authz-req}

Uma solicitação AuthZ deve incluir um assunto em cujo nome a solicitação está sendo feita, o(s) recurso(s) que o assunto está tentando acessar, a ação que o assunto está tentando executar no recurso e o ambiente em que a operação está prestes a ocorrer. No caso específico da autenticação da Adobe Primetime, esses elementos correspondem a:

| Elemento XACML | Corresponde a |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| Assunto | O principal identificado pela Sessão Autenticada, referenciado pelo AttributeValue &#39;subject-token&#39; da asserção SAML. |
| Recurso | Um URI para o recurso protegido. |
| Ação | EXIBIR. |
| Ambiente | Inclui o endereço IP do cliente que fez a solicitação, conforme visualizado pela controladora do armazenamento. |



O SP neste ponto deve preparar um XACML Authorization DecisionQuery e enviá-lo (via HTTP POST) para o PDP (Policy Decisioning Point) (anteriormente acordado) para o IdP. Abaixo está um exemplo de uma Solicitação XACML simples (consulte a especificação principal do XACML):

```XML
POST https://authz.site.com/XACML_endpoint
<Request  xmlns="urn:oasis:names:tc:xacm:2.0:context:schema:os"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="urn:oasis:names:tc:xacml:2.0:context:schema:os
http://docs.oasis-open.org/xacml/access_control-xacml-2.0-context-schema-os.xsd">
<Subject>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-token"
        DataType="http://www.w3.org/2001/XMLSchema#base64Binary">
      <AttributeValue>{Base64 Data}</AttributeValue>
   </Attribute>
</Subject>
<Resource>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id"
        DataType="http://www.w3.org/2001/XMLSchema#anyURI">
<AttributeValue>urn:tve:tms:1234</AttributeValue>
   </Attribute>
</Resource>
<Action>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id"
        DataType="http://www.w3.org/2001/XMLSchema#string">
       <AttributeValue>VIEW</AttributeValue>
   </Attribute>
</Action>
<Environment>
   <Attribute
       AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address"
       DataType="http://www.w3.org/2001/XMLSchema#string">
      <AttributeValue>1.2.3.4</AttributeValue>
   </Attribute>
</Environment>
</Request>
```


Depois de receber a solicitação AuthZ, o PDP do MVPD avalia a solicitação e determina se o assunto deve ter permissão para executar a ação solicitada no recurso. O MVPD retorna uma resposta com uma Decisão, Código de status e mensagem, conforme descrito em A resposta da autorização abaixo.

## A Resposta de Autorização {#authz-response}

A resposta à solicitação AuthZ vem depois que o MVPD avalia a solicitação e aplica as regras de negócios solicitadas para determinar se o assunto tem permissão para executar a ação solicitada no recurso . A resposta retornada à autenticação da Adobe Primetime é expressa novamente seguindo a especificação principal de XACML com uma Decisão, um código de status, mensagem e Obrigações que a controladora tem como Ponto de Aplicação de Política (PEP). Este é um exemplo de Resposta:

```XML
<Response xmlns="urn:oasis:names:tc:xacml:2.0:context:schema:os">
  <Result>
  <Decision>Permit</Decision>
  <Status>
     <StatusCode Value="urn:oasis:names:tc:xacml:1.0:status:ok"/>
     <StatusMessage>ok</StatusMessage>
  </Status>
  <xacml:Obligations     
          xmlns:xacml="urn:oasis:names:tc:xacml:2.0:policy:schema:os">
     <xacml:Obligation    
              ObligationId="urn:cablelabs:olca:1.0:obligations:log"
              FulfillOn="Permit" />
  </xacml:Obligations>
 </Result>
</Response>
```

Veja a seguir uma lista de obrigações de NEGAÇÃO que a autenticação da Adobe Primetime suporta e permite que os programadores atendam:

* **urn:tve:xacml:2.0:obligations:restrict-pc** - O Assinante não passou em uma verificação de controle dos pais e o SP deve tomar as medidas apropriadas para restringir o acesso a esse conteúdo.

* **urn:tve:xacml:2.0:obligations:atualizar** - O Assinante não tem um nível de assinatura apropriado.  É necessário atualizar a assinatura para acessar o conteúdo.

A autenticação da Adobe Primetime é compatível com o seguinte **PERMITE** Obrigações e condições para que os programadores as cumpram:

* **urn:cablelabs:olca:1.0:obligations:log** - A Adobe Pass registra a transação e pode disponibilizá-la por meio do mecanismo de relatório acordado.

* **urn:cablelabs:olca:1.0:obligations:re-authz** - A autenticação da Adobe Primetime atualiza a autorização novamente em n segundos (especificado como um argumento para a Obrigação por meio de uma Atribuição de atributo XACML - consulte a especificação principal de XACML , Seção 5.46).

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->