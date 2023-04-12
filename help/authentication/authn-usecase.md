---
title: Autenticação MVPD
description: Autenticação MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---


# Autenticação MVPD {#mvpd-authn}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#mvpd-authn-overview}

A função do provedor de serviços (SP) real é mantida por um Programador, mas a autenticação da Adobe Primetime serve como proxy da controladora de armazenamento para esse Programador. Usar a autenticação da Adobe Primetime como um intermediário permite que tanto MVPDs quanto Programadores evitem a necessidade de personalizar seus processos de direito caso a caso.

As etapas abaixo apresentam a sequência de eventos, usando a autenticação da Adobe Primetime, quando um Programador solicita a autenticação de um MVPD compatível com SAML. Observe que o componente Adobe Primetime authentication Access Enabler está ativo no cliente do usuário/assinante. A partir daí, o Ativador de acesso facilita todas as etapas do fluxo de autenticação.

1. Quando o usuário solicita acesso a conteúdo protegido, o Ativador de Acesso inicia a autenticação (AuthN) em nome do Programador (SP).
1. O aplicativo da controladora apresenta um &quot;Seletor de MVPD&quot; ao usuário para obter o provedor de TV paga (MVPD). O SP redireciona o navegador do usuário para o serviço de provedor de identidade (IdP) do MVPD selecionado.  Isso é &quot;**Logon iniciado pelo programador**&quot;.  O MVPD envia a resposta do IdP para o serviço de asserção do Adobe SAML, onde é processado.
1. Por fim, o Access Enabler redireciona o navegador de volta para o site da controladora de armazenamento, informando à controladora o status (sucesso / falha) da solicitação AuthN.

## A Solicitação de Autenticação {#authn-req}

Conforme apresentado nas etapas acima, durante o fluxo AuthN, um MVPD deve aceitar uma solicitação AuthN baseada em SAML e enviar uma resposta SAML AuthN.

O [Especificação da Interface de Autenticação e Autorização de Acesso Online a Conteúdo (OLCA)](https://www.cablelabs.com/specifications/search?query=&amp;category=&amp;subcat=&amp;doctype=&amp;content=false&amp;archives=false){target=_blanck} O apresenta uma solicitação e uma resposta padrão do AuthN. Embora a autenticação da Adobe Primetime não exija que os MVPDs baseiem suas mensagens de direito nesse padrão, analisar a especificação pode fornecer informações sobre os atributos principais necessários para uma transação AuthN.

>[!NOTE]
>
>A solicitação AuthN que um MVPD recebe com a autenticação da Adobe Primetime contém uma assinatura digital. No entanto, o exemplo abaixo não mostra uma assinatura, por motivos de brevidade. Para ver um exemplo que mostra uma assinatura digital, consulte o exemplo em [a resposta de autenticação](#authn-response) nas seções a seguir.

Solicitação de autenticação SAML de exemplo:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<samlp:AuthnRequest  
    AssertionConsumerServiceURL=http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer          
    Destination=http://idp.com/SSOService
    ForceAuthn="false"
    ID="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
    IsPassive="false"
    IssueInstant="2010-08-03T14:14:54.372Z"
    ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
    Version="2.0"
    xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
        http://saml.sp.adobe.adobe.com
    </saml:Issuer>
    <ds:Signature xmlns:ds=_signature_block_goes_here_
    </ds:Signature>
    <samlp:NameIDPolicy
        AllowCreate="true"
        Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
        SPNameQualifier="http://saml.sp.adobe.adobe.com"/>
</samlp:AuthnRequest> 
```

A tabela abaixo explica os atributos e tags que precisam estar em uma solicitação de autenticação, com os valores padrão esperados.

**Detalhes da solicitação de autenticação SAML**

| samlp:AuthnRequest | &lt;authnrequest> emitido pelo Provedor de Serviços ao Provedor de Identidade. |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AssertionConsumerServiceURL | Esse é o terminal Adobe para usar na resposta subsequente. Valor padrão: **http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer** |
| Destino | Uma referência de URI que indica o endereço para o qual esta solicitação foi enviada. Isso é útil para impedir o encaminhamento mal-intencionado de solicitações para destinatários não intencionais, uma proteção exigida por alguns vínculos de protocolo. Se estiver presente, o recipient real DEVE verificar se a referência de URI identifica o local em que a mensagem foi recebida. Caso contrário, a solicitação DEVE ser descartada. Alguns vínculos de protocolo podem exigir o uso desse atributo. |
| ForceAuthn | O atributo ForceAuthn, se presente com um valor true, obriga o provedor de identidade a estabelecer essa identidade recentemente, em vez de depender de uma sessão existente que possa ter com o principal. |
| ID | Um identificador para a solicitação. Consulte [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} seção 1.3.4 para mais pormenores. |
| IsPassive | Um valor booleano. Se &quot;true&quot;, o provedor de identidade e o próprio agente do usuário NÃO DEVEM assumir visivelmente o controle da interface do usuário do solicitante e interagir com o apresentador de maneira perceptível. Se um valor não for fornecido, o padrão será &quot;false&quot;. |
| IssueInstant | O momento da emissão da resposta. O valor de hora é codificado em UTC, conforme descrito em [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} Seção 1.3.3. |
| ProtocolBinding | Uma referência de URI que identifica um vínculo de protocolo SAML a ser usado ao retornar &lt;response> mensagem. Consulte [SAMLBind] para obter mais informações sobre vínculos de protocolo e referências de URI definidas para eles. Valor padrão : urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST |
| Versão | A versão desta solicitação. |
| saml:Emissor | Identifica a entidade que gerou a mensagem de resposta. (Para mais informações sobre este elemento, consulte SAML core 2.0-os Seção 2.2.5) |
| ds:Signature | Uma assinatura XML que protege a integridade da asserção e autentica o emissor dessa asserção, conforme descrito na Seção 5 no SAML core 2.0-os |
| samlp:NameIDPpolicy | Especifica restrições no identificador de nome a ser usado para representar o assunto solicitado. |
| AllowCreate | Um valor booleano usado para indicar se o provedor de identidade tem permissão, durante o cumprimento da solicitação, para criar um novo identificador para representar o principal. Padrão: true |
| Formato | Especifica a referência de URI correspondente a um formato de identificador de nome Padrão: urn:oasis:names:tc:SAML:2.0:nameid-format:Adobe transient recomenda: urn:oasis:names:tc:SAML:2.0:nameid-format:persistente |
| SPNameQualifier | Especifica opcionalmente que o identificador do assunto da asserção seja retornado (ou criado) no namespace de um provedor de serviços diferente do solicitante. Padrão : http://saml.sp.adobe.adobe.com |

## A resposta de autenticação {#authn-response}

Depois de receber e manipular a solicitação de autenticação, o MVPD deve enviar uma resposta de autenticação.

**Exemplo de resposta de autenticação SAML**

```XML
<?xml version="1.0" encoding="UTF-8"?> 
<samlp:Response Destination="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                ID="_0ac3a9dd5dae0ce05de20912af6f4f83a00ce19587"                             
                InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                IssueInstant="2010-08-17T11:17:50Z" Version="2.0"              
                xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
                xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
                xmlns:xs="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
             http://idp.com/SSOService
    </saml:Issuer>
    <samlp:Status>
       <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    <saml:Assertion ID="pfxb0662d76-17a2-a7bd-375f-c11046a86742"
                   IssueInstant="2010-08-17T11:17:50Z"
                   Version="2.0">
        <saml:Issuer>http://idp.com/SSOService</saml:Issuer>
        <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
          <ds:SignedInfo>
            <ds:CanonicalizationMethod
                     Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
            <ds:SignatureMethod
                     Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
            <ds:Reference URI="#pfxb0662d76-17a2-a7bd-375f-c11046a86742">
              <ds:Transforms>
                 <ds:Transform
                    Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>        
                 <ds:Transform
                            Algorithm=http://www.w3.org/2001/10/xml-exc-c14n#"/>
              </ds:Transforms>
              <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
              <ds:DigestValue>LgaPI2ASx/fHsoq0rB15Zk+CRQ0=</ds:DigestValue>
            </ds:Reference>
          </ds:SignedInfo>
          <ds:SignatureValue>
                POw/mCKF__shortened_for_brevity__9xdktDu+iiQqmnTs/NIjV5dw==
          </ds:SignatureValue>
          <ds:KeyInfo>
            <ds:X509Data>
                <ds:X509Certificate>
                 MIIDVDCCAjygAwIBA__shortened_for_brevity_utQ==
                </ds:X509Certificate>
            </ds:X509Data>
          </ds:KeyInfo>
      </ds:Signature>
      <saml:Subject>
        <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
                     SPNameQualifier="https://saml.sp.auth.adobe.com">
            _5afe9a437203354aa8480ce772acb703e6bbb8a3ad
        </saml:NameID>
        <saml:SubjectConfirmation
                     Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
            <saml:SubjectConfirmationData
                  InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                  NotOnOrAfter="2010-08-17T11:22:50Z"                                          
                  Recipient="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"/>
           </saml:SubjectConfirmation>
       </saml:Subject>
       <saml:Conditions NotBefore="2010-08-17T11:17:20Z"
                        NotOnOrAfter="2010-08-17T19:17:50Z">
           <saml:AudienceRestriction>
              <saml:Audience>https://saml.sp.auth.adobe.com</saml:Audience>
           </saml:AudienceRestriction>
       </saml:Conditions>
       <saml:AuthnStatement AuthnInstant="2010-08-17T11:17:50Z"
                   SessionIndex="_1adc7692e0fffbb1f9b944aeafce62aaa7d770cd9e">
        <saml:AuthnContext>
            <saml:AuthnContextClassRef>
                   urn:oasis:names:tc:SAML:2.0:ac:classes:Password
            </saml:AuthnContextClassRef>
        </saml:AuthnContext>
    </saml:AuthnStatement>
  </saml:Assertion>
</samlp:Response>
```


Na amostra acima, o Adobe SP espera buscar a ID do usuário do Subject/NameId. O Adobe SP pode ser configurado para obter a ID de usuário de um atributo definido personalizado; a resposta deve conter um elemento como o seguinte:

```XML
<saml:AttributeStatement>
     <saml:Attribute Name="guid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
         <saml:AttributeValue xsi:type="xs:string">
               71C69B91-F327-F185-F29E-2CE20DC560F5
         </saml:AttributeValue>
    </saml:Attribute>
</saml:AttributeStatement>
```

**Detalhes da resposta de autenticação SAML**
| samlp:Response | Resposta recebida pela autenticação da Adobe Primetime.                                                                                                                                                                                                                                                                                                                                                                                                                       | |—|—| | Destino | Uma referência de URI que indica o endereço para o qual esta solicitação foi enviada. Isso é útil para impedir o encaminhamento mal-intencionado de solicitações para destinatários não intencionais, uma proteção exigida por alguns vínculos de protocolo. Se estiver presente, o recipient real DEVE verificar se a referência de URI identifica o local em que a mensagem foi recebida. Caso contrário, a solicitação DEVE ser descartada. Alguns vínculos de protocolo podem exigir o uso desse atributo. | | ID | Um identificador para a solicitação. É do tipo xs:ID e DEVE cumprir os requisitos especificados no ponto 1.3.4 do [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} para exclusividade do identificador. Os valores do atributo ID em uma solicitação e do atributo InResponseTo na resposta correspondente DEVEM corresponder.                                                                                                                                                                                         | | InResponseTo | A identificação de uma mensagem de protocolo SAML em resposta à qual uma entidade de certificação pode apresentar a afirmação. O valor deve ser igual ao do atributo ID enviado na Solicitação de autenticação. Consulte SAML core 2.0-os | | IssueInstant | O momento da emissão do pedido.                                                                                                                                                                                                                                                                                                                                                                                                                                  | | Versão | A versão do pedido.                                                                                                                                                                                                                                                                                                                                                                                                                                                | | saml:Emissor | Identifica a entidade que gerou a mensagem de solicitação. (Para mais informações sobre este elemento, ver Seção 2.2.5. Núcleo 2.0-os do SAML) | | samlp:Status | Um código que representa o status da solicitação correspondente.                                                                                                                                                                                                                                                                                                                                                                                                               | | samlp:StatusCode | Um código que representa o status da atividade realizada em resposta à solicitação correspondente.                                                                                                                                                                                                                                                                                                                                                                       | | saml:Asserção | Este tipo especifica as informações de base comuns a todas as asserções.                                                                                                                                                                                                                                                                                                                                                                                                        | | ID | O identificador dessa asserção.                                                                                                                                                                                                                                                                                                                                                                                                                                         | | Versão | A versão desta afirmação.                                                                                                                                                                                                                                                                                                                                                                                                                                             | | IssueInstant | O momento da emissão do pedido.                                                                                                                                                                                                                                                                                                                                                                                                                                  | | ds:Assinatura | Uma assinatura XML que protege a integridade da asserção e autentica o emitente, conforme descrito na Seção 5 do SAML core 2.0-os | | ds:SignedInfo | A estrutura de SignedInfo inclui o algoritmo de canonicalização, um algoritmo de assinatura e uma ou mais referências. O elemento SignedInfo pode conter um atributo de ID opcional que permitirá que ele seja referenciado por outras assinaturas e objetos. Consulte Sintaxe e processamento de assinatura XML | | ds:CanonicalizationMethod | CanonicalizationMethod é um elemento necessário que especifica o algoritmo de canonicalização aplicado ao elemento SignedInfo antes de executar cálculos de assinatura. Consulte Sintaxe e processamento de assinatura XML | | ds:SignatureMethod | SignatureMethod é um elemento necessário que especifica o algoritmo usado para geração e validação de assinatura. Este algoritmo identifica todas as funções criptográficas envolvidas na operação de assinatura (por exemplo, hash, algoritmos de chave pública, MACs, preenchimento etc.) Consulte Sintaxe e processamento de assinatura XML | | ds:Referência | Referência é um elemento que pode ocorrer uma ou mais vezes. Especifica um algoritmo de compilação e um valor de compilação, e opcionalmente um identificador do objeto que está sendo assinado, o tipo do objeto e/ou uma lista de transformações a serem aplicadas antes da compilação. Consulte Sintaxe e processamento de assinatura XML | | ds:Transformações | O elemento opcional Transforms contém uma lista ordenada de elementos Transform ; esses itens descrevem como o assinante obteve o objeto de dados que foi digerido. A saída de cada Transformação serve como entrada para a próxima Transformação. A entrada para a primeira Transform é o resultado do cancelamento da referência do atributo URI do elemento Reference. A saída da última Transformação é a entrada para o algoritmo DigestMethod. Consulte Sintaxe e processamento de assinatura XML | | ds:DigestMethod | DigestMethod é um elemento necessário que identifica o algoritmo de compilação a ser aplicado ao objeto assinado. Consulte Sintaxe e processamento de assinatura XML | | ds:DigestValue | DigestValue é um elemento que contém o valor codificado do resumo. O resumo é sempre codificado usando base64. Consulte Sintaxe e processamento de assinatura XML | | ds:SignatureValue | O elemento SignatureValue contém o valor real da assinatura digital; sempre é codificado usando base64. Consulte Sintaxe e processamento de assinatura XML | | ds:KeyInfo | KeyInfo é um elemento opcional que permite ao(s) destinatário(s) obter a chave necessária para validar a assinatura. Consulte Sintaxe e processamento de assinatura XML | | ds:X509Dados | Um elemento X509Data em KeyInfo contém um ou mais identificadores de chaves ou certificados X509. Consulte Sintaxe e processamento de assinatura XML | | d: Certificado X509 | O elemento de certificado X509que contém um código base64 [X509v3] certificate | | saml:Assunto | Objeto da declaração ou declarações da declaração.                                                                                                                                                                                                                                                                                                                                                                                                                          | | saml:NameID | &lt;nameid> é do tipo NameIDType (ver Seção 2.2.2 no SAML core 2.0-os) e é usado em várias construções de asserção SAML, como o &lt;subject> e &lt;subjectconfirmation> e em várias mensagens de protocolo.                                                                                                                                                                                                                                           | | Formato | Uma referência de URI que representa a classificação das informações de identificador com base em sequência.                                                                                                                                                                                                                                                                                                                                                                                    | | SPNameQualifier | Além disso, qualifica um nome com o nome de um provedor de serviços ou afiliação de provedores. Este atributo fornece um meio adicional para federar os nomes com base na(s) parte(s) confiadora(s).                                                                                                                                                                                                                                                                      | | saml:SubjectConfirmation | Informações que permitem confirmar o assunto. Se for fornecida mais do que uma confirmação, a satisfação de qualquer uma delas é suficiente para confirmar o assunto para efeitos de aplicação da asserção.                                                                                                                                                                                                                                                    | | saml:SubjectConfirmationData | Informações adicionais de confirmação a utilizar por um método de confirmação específico. Por exemplo, o conteúdo típico desse elemento pode ser um <!--<ds:KeyInfo>--> elemento conforme definido na especificação da sintaxe e do processamento de assinatura XML | | NotOnOrAfter | Momento em que o assunto deixou de poder ser confirmado.                                                                                                                                                                                                                                                                                                                                                                                                            | | Destinatário | URI que especifica a entidade ou o local em que a entidade de certificação pode apresentar a afirmação. Por exemplo, esse atributo pode indicar que a asserção deve ser entregue a um terminal de rede específico para impedir que um intermediário a redirecione para outro lugar.                                                                                                                                                                                   | | saml:Condições | &lt;condition> serve como um ponto de extensão para novas condições.                                                                                                                                                                                                                                                                                                                                                                                                   | | NotBefore | O atributo NotBefore especifica o momento em que o intervalo de validade começa.                                                                                                                                                                                                                                                                                                                                                                                  | | saml:AudienceRestriction | &lt;audiencerestriction> especifica que a asserção é endereçada a um ou mais públicos-alvo específicos identificados por &lt;audience> elementos.                                                                                                                                                                                                                                                                                                                           | | saml:Audience | Uma referência de URI que identifica um público-alvo pretendido.                                                                                                                                                                                                                                                                                                                                                                                                                      | | saml:AuthnStatement | Uma declaração de autenticação.                                                                                                                                                                                                                                                                                                                                                                                                                                               | | AuthnInstant | Especifica a hora em que a autenticação ocorreu.                                                                                                                                                                                                                                                                                                                                                                                                                 | | ÍndiceSessão | Especifica o índice de uma sessão específica entre o responsável principal identificado pelo assunto e a autoridade de autenticação.                                                                                                                                                                                                                                                                                                                                              | | saml:AuthnContext | O contexto usado pela autoridade de autenticação até o evento de autenticação que rendeu esta instrução, inclusive.                                                                                                                                                                                                                                                                                                                                                 | | saml:AuthnContextClassRef | Uma referência de URI que identifica uma classe de contexto de autenticação que descreve a declaração de contexto de autenticação que se segue. |