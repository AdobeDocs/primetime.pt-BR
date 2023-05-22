---
title: Autorização MVPD
description: Autorização MVPD
exl-id: 215780e4-12b6-4ba6-8377-4d21b63b6975
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Autorização MVPD

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Visão geral {#mvpd-authz-overview}

A autorização (AuthZ) é executada através de comunicações back-channel (servidor para servidor) entre um servidor back-end hospedado em Adobe e o endpoint MVPD AuthZ.

Para solicitações AuthZ, o endpoint de autorização deve ser capaz de processar pelo menos os seguintes parâmetros:

* **Uid**. A ID de usuário recebida da etapa de autenticação.

* **ID do recurso**. Uma string que identifica um determinado recurso de conteúdo. Essa ID de recurso é especificada pelo Programador e o MVPD deve reforçar as regras de negócios desses recursos (por exemplo, verificando se o usuário está inscrito em um determinado canal).

Além de determinar se o usuário está autorizado, a resposta deve incluir o TTL (time-to-live) dessa autorização, ou seja, quando a autorização expira. Se o TTL não for definido, a solicitação AuthZ falhará.  Por esse motivo, **o TTL é uma configuração obrigatória no lado da autenticação do Adobe Primetime**, a fim de abranger o caso em que um MVPD não inclua o TTL no seu pedido.

## A solicitação de autorização {#authz-req}

Uma solicitação AuthZ deve incluir um assunto em nome do qual a solicitação está sendo feita, os recursos que o sujeito está tentando acessar, a ação que o sujeito está tentando executar no recurso e o ambiente no qual a operação está prestes a ocorrer. No caso específico da autenticação Adobe Primetime, esses elementos correspondem a:

| Elemento XACML | Corresponde a |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| Assunto | A entidade de segurança identificada pela Sessão Autenticada, referenciada pelo AttributeValue &quot;subject-token&quot; da asserção SAML. |
| Recurso | Um URI para o recurso protegido. |
| Ação | EXIBIR. |
| Ambiente | Inclui o endereço IP do cliente solicitante, conforme visto pela controladora. |



A controladora de armazenamento neste ponto deve preparar uma consulta de decisão de autorização XACML e enviá-la (via POST HTTP) ao ponto de decisão de política (PDP) (previamente acordado) para o IdP. Abaixo está um exemplo de uma solicitação XACML simples (consulte a especificação principal XACML):

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


Depois de receber a solicitação AuthZ, o PDP do MVPD avalia a solicitação e determina se o assunto deve ter permissão para executar a ação solicitada no recurso. O MVPD retorna uma resposta com uma Decisão, Código de status e mensagem, conforme descrito em A resposta de autorização abaixo.

## A Resposta de Autorização {#authz-response}

A resposta à solicitação de AuthZ vem depois que o MVPD avalia a solicitação e aplica as regras de negócios solicitadas para determinar se o sujeito tem permissão para executar a ação solicitada no recurso. A resposta retornada à autenticação da Adobe Primetime é expressa novamente seguindo a especificação principal da XACML com uma Decisão, um Código de status, uma mensagem e Obrigações que a controladora tem como PEP (Ponto de aplicação de política). Este é um exemplo de Resposta:

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

Veja a seguir uma lista de Obrigações de NEGAÇÃO que a autenticação do Adobe Primetime aceita e permite que os Programadores cumpram:

* **urn:tve:xacml:2.0:obligations:restrict-pc** - O Assinante não passou em uma verificação de controle dos pais e o SP deve tomar as medidas apropriadas para restringir o acesso a esse conteúdo.

* **urn:tve:xacml:2.0:obligations:atualização** - O Assinante não tem um nível de assinatura apropriado.  É necessário atualizar a assinatura para acessar o conteúdo.

A autenticação do Adobe Primetime é compatível com o seguinte **PERMITIR** Obrigações e permite aos programadores cumprirem-nas:

* **urn:cablelabs:olca:1.0:obligations:log** - A Adobe Pass registra a transação e pode disponibilizá-la por meio do mecanismo de relatório acordado.

* **urn:cablelabs:olca:1.0:obligations:reautenticação** - A autenticação do Adobe Primetime atualiza a autorização novamente em n segundos (especificado como um argumento para a Obrigação por meio de uma Atribuição XACML - consulte Especificação principal XACML , Seção 5.46).

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->
