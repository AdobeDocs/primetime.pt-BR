---
title: Serviço Web MVPD Proxy
description: Serviço Web MVPD Proxy
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# Serviço Web MVPD Proxy {#proxy-mvpd-wbservice}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral {#overview-proxy-mvpd-webserv}

Um &quot;MVPD Proxy&quot; é um MVPD que, além de gerenciar sua própria integração com a autenticação da Adobe Primetime, também gerencia o processo de direito em nome de um grupo de &quot;MVPDs Proxied&quot; associados. Este acordo é transparente para os programadores.

Para implementar o recurso ProxyMVPD, a autenticação da Adobe Primetime fornece serviços Web RESTful, com os quais ProxyMVPDs podem enviar e recuperar listas de ProxiedMVPDs. O protocolo usado para essa API pública é REST HTTP, com as seguintes suposições:

* O MVPD de Proxy usa o método HTTP GET para recuperar a lista de MVPDs integrados atuais.
* O MVPD do Proxy usa o método POST HTTP para atualizar a lista dos MVPDs suportados.

## Serviços MVPD de proxy {#proxy-mvpd-services}

* [Recuperar MVPDs proxy](#retriev-proxied-mvpds)
* [Enviar MVPDs proxy](#submit-proxied-mvpds)

### Recuperar MVPDs proxy {#retriev-proxied-mvpds}

Recupera a lista atual de MVPDs Proxied para o ProxyMVPD identificado pelo parâmetro apikey.

| Endpoint | Chamado por | Cabeçalhos de solicitação | Método HTTP | Resposta HTTP |
|---|---|---|---|---|
| &lt;fqdn>/control/v1/proxiedMvpds | ProxyMVPD | apikey (Obrigatório) | GET | <ul><li> 200 (ok) - A solicitação foi processada com êxito e a resposta contém uma lista de ProxiedMVPDs no formato XML</li><li>401 (não autorizado) - Autenticação do usuário necessária ou não concedida para credenciais fornecidas.  Indica um dos seguintes:<ul><li>O token apikey não está presente no cabeçalho da solicitação</li><li>A solicitação se origina de um endereço IP que não está presente na lista de permissões</li><li>O token não é válido</li></ul></li><li>403 (proibido) - Indica que a operação não é suportada para os parâmetros fornecidos ou que o MVPD proxy não está definido como proxy ou está ausente</li><li>405 (método não permitido) - Um método HTTP diferente de GET ou POST foi usado. O método HTTP geralmente não é aceito ou não é aceito para esse endpoint específico.</li><li>500 (erro interno do servidor) - Um erro foi gerado no lado do servidor durante o processo de solicitação.</li></ul> |

Exemplo de ondulação:

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`


Exemplo de resposta XML:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```

### Enviar MVPDs proxy {#submit-proxied-mvpds}

Empurra uma matriz de MVPDs integrados ao MVPD do Proxy identificado pelo parâmetro apikey.

| Endpoint | Chamado por | Cabeçalhos de solicitação | Método HTTP | Resposta HTTP |
|:------------------------------:|:---------:|:--------------------------------------------:|:-----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| &lt;fqdn>/control/v1/proxiedMvpds | ProxyMVPD | apikey (Obrigatório) proxied-mvpds (Obrigatório) | POST | <ul><li>201 (criado) - O push foi processado com êxito</li><li>400 (solicitação incorreta) - O servidor não sabe como processar a solicitação:<ul><li>O XML de entrada não adere ao schema publicado nesta especificação</li><li>Os mvpds proxies não têm ids exclusivas</li><li>O requestorIds enviado não existe Outro motivo do contêiner Servlet para o código de resposta 400</li></ul><li>401 (não autorizado) - A apikey não é válida ou o IP do chamador não está na lista de permissões</li><li>403 (proibido) - Indica que a operação não é suportada para os parâmetros fornecidos ou que o MVPD proxy não está definido como proxy ou está ausente</li><li>405 (método não permitido) - Um método HTTP diferente de GET ou POST foi usado. O método HTTP geralmente não é aceito ou não é aceito para esse endpoint específico.</li><li>500 (erro interno do servidor) - Um erro foi gerado no lado do servidor durante o processo de solicitação.</li></ul> |

Exemplo de ondulação:

`curl -X POST -H "apikey: <API_KEY>" "https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds" -d "proxied-mvpds=%3CproxiedMvpds%3E%3CproxiedMvpd%3E%3CdisplayName%3EFirst%20MVPD%20Name%3C%2FdisplayName%3E%3Cid%3EfirstMVPDId%3C%2Fid%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3C%2FproxiedMvpd%3E%3CproxiedMvpd%3E%3Cid%20ProviderID%3D%22ProviderID_Value_Sent_On_IdPEntry%22%3EmvpdPickerId%3C%2Fid%3E%3CdisplayName%3EMVPD%20Name%20Two%3C%2FdisplayName%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3CrequestorIds%3E%3CrequestorId%3ETHE_REQUESTOR_ID%3C%2FrequestorId%3E%3C%2FrequestorIds%3E%3C%2FproxiedMvpd%3E%3C%2FproxiedMvpds%3E"`



Exemplo XML:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```


### Frequência de publicação {#posting-frequency}

A autenticação da Adobe Primetime recomenda que o ProxyMVPDs deve encaminhar sua lista de ProxiedMVPDs somente quando houver uma alteração do push anterior.

### Excluindo MVPDs Proxied {#delete-proxied-freqency}

Se o ProxyMVPD enviar um registro XML com uma lista ProxiedMVPDs vazia, essa lista vazia será armazenada em nosso sistema como qualquer lista, excluindo assim efetivamente a lista anterior.



## Formato XSD {#xsd-format}

O Adobe definiu o seguinte formato aceito para postar/recuperar MVPDs proxy de/para nosso serviço público da Web:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns:pxm="http://tve.adobe.com/data/proxiedmvpd"
           targetNamespace="http://tve.adobe.com/data/proxiedmvpd"
           elementFormDefault="qualified"
           version="1.0">
    <xs:complexType name="iframeSize">
        <xs:all>
            <xs:element name="iframeHeight" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeWidth" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
        </xs:all>
    </xs:complexType>
    <xs:complexType name="requestorIds">
        <xs:annotation>
            <xs:documentation>List of requestors/programmers integrated with the proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:sequence>
            <xs:element name="requestorId" type="xs:string" minOccurs="1" maxOccurs="unbounded" nillable="false">
                <xs:annotation>
                    <xs:documentation>The requestor/programmer identifier recognized by Adobe</xs:documentation>
                </xs:annotation>
            </xs:element>
        </xs:sequence>
    </xs:complexType>
    <xs:complexType name="proxiedMvpd">
        <xs:all>
            <xs:element name="id" minOccurs="1" maxOccurs="1" nillable="false">
                <xs:annotation>
                    <xs:documentation>The id must conform to the regular expression: ([a-zA-Z0-9]+((\-)|[_])*)</xs:documentation>
                </xs:annotation>
                <xs:complexType>
                    <xs:simpleContent>
                        <xs:extension base="xs:string">
                            <xs:attribute name="ProviderID">
                                <xs:simpleType>
                                    <xs:restriction base="xs:string">
                                        <xs:minLength value="1"/>
                                        <xs:maxLength value="128"/>
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:attribute>
                        </xs:extension>
                    </xs:simpleContent>
                </xs:complexType>
            </xs:element>
            <xs:element name="displayName" type="xs:string" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="logoURL" type="xs:anyURI" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeSize" type="pxm:iframeSize" minOccurs="0" maxOccurs="1"/>
            <xs:element name="requestorIds" type="pxm:requestorIds" minOccurs="0" maxOccurs="1"/>
        </xs:all>
    </xs:complexType>
    <xs:element name="proxiedMvpds">
        <xs:annotation>
            <xs:documentation>List of Proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:complexType>
            <xs:sequence>
                <xs:element name="proxiedMvpd" type="pxm:proxiedMvpd" minOccurs="0" maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

**Observações sobre os elementos:**

* `id` (obrigatório) - O ID MVPD Proxied deve ser uma string relevante para o nome do MVPD, usando qualquer um dos seguintes caracteres (pois será exposto a Programadores para fins de rastreamento):
   * Qualquer caractere alfanumérico, sublinhado (&quot;_&quot;) e hífen (&quot;-&quot;).
   * A idID deve estar em conformidade com a seguinte expressão regular:
      `(a-zA-Z0-9((-)|_)*)`

      Portanto, deve ter pelo menos um caractere, começar com uma letra e continuar com qualquer letra, dígito, traço ou sublinhado.

* `iframeSize` (opcional) - o elemento iframeSize é opcional e define o tamanho do iFrame se a página de autenticação do MVPD tiver que estar em um iFrame. Caso contrário, se o elemento iframeSize não estiver presente, a autenticação ocorrerá em uma página de redirecionamento completo do navegador.
* `requestorIds` (opcional) - Os valores requestorIds serão fornecidos pelo Adobe. Um requisito é que um MVPD proxy deve ser integrado com pelo menos um requestorId. Se a tag &quot;requestorIds&quot; não estiver presente no elemento MVPD proxy, esse MVPD proxy será integrado a todos os solicitantes disponíveis integrados no MVPD proxy.
* `ProviderID` (opcional) - Quando o atributo ProviderID está presente no elemento id , o valor de ProviderID será enviado na solicitação de autenticação SAML para o MVPD Proxy como a ID MVPD / SubMVPD Proxied (em vez do valor da id). Nesse caso, o valor da id será usado somente no seletor de MVPD apresentado na página do Programador e internamente pela autenticação da Adobe Primetime. O comprimento do atributo ProviderID deve estar entre 1 e 128 caracteres.

## Segurança {#security}

Para que um pedido seja considerado válido, deve respeitar as seguintes regras:

* O cabeçalho da solicitação deve conter o parâmetro apikey de segurança. (Essa é uma chave de aplicativo que identificará exclusivamente as chamadas do MVPD do Proxy.)
* A solicitação deve vir de um endereço IP específico que foi permitido.
* A solicitação deve ser enviada pelo protocolo SSL.

Adobe fornecerá o valor (estático) do token. Esse valor é usado no processo de autenticação e autorização.  Todos os parâmetros presentes no cabeçalho da solicitação que não estão listados acima serão ignorados.

Exemplo de ondulação:

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`

## Endpoints de serviço da Web MVPD de proxy para os ambientes de autenticação da Adobe Primetime {#proxy-mvpd-wevserv-endpoints}

* **URL de produção:** https://mgmt.auth.adobe.com/control/v1/proxiedMvpds
* **URL de preparo:** https://mgmt.auth-staging.adobe.com/control/v1/proxiedMvpds
* **URL de pré-produção:** https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds
* **URL de preparação pré-qual:** https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds

<!--
>[!RELATEDINFORMATION]
>* [Proxy MVPD SAML integration](/help/authentication/proxy-mvpd-saml-int.md)
>* [User metadata exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Technical paper](/help/authentication/technical-paper.md)
>* [Adobe Primetime Authentication glossary](/help/authentication/glossary.md)
-->
