---
title: Troca de Metadados de Usuário do MVPD
description: Troca de Metadados de Usuário do MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Troca de Metadados de Usuário do MVPD

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#intro-user-metadata-exchange}

Os MVPDs mantêm metadados específicos do usuário sobre seus clientes que, em alguns casos, são compartilhados com Programadores. O objetivo da autenticação da Adobe Primetime é intermediar uma troca desses &quot;metadados de usuário&quot;, mas não impor qualquer tipo de regra relacionada à troca. As regras de troca são para os MVPDs trabalharem com seus parceiros de programação.

Os tipos de metadados de usuário disponíveis para troca incluem:

* Código postal
* Classificação máxima (VChip ou MPAA)
* ID de usuário
* ID da família
* ID do canal

Com esse recurso, os MVPDs e Programadores podem implementar casos de uso especiais, como controle dos pais. Por exemplo, um MVPD pode passar dados de classificação dos pais para um Programador, que usa esses dados para filtrar as opções de visualização disponíveis para um usuário.

Pontos principais de metadados do usuário:

* O MVPD passa os metadados do usuário para o aplicativo do Programador durante os fluxos de autenticação e autorização
* A autenticação Adobe Primetime salva os valores de metadados nos tokens AuthN e AuthZ
* A autenticação Adobe Primetime pode normalizar valores para MVPDs que fornecem metadados de usuário em diferentes formatos
* Alguns parâmetros podem ser criptografados usando a chave do Programador
* Valores específicos são disponibilizados pelo Adobe, por meio de uma alteração de configuração

>[!NOTE]
>
>Metadados do usuário é uma extensão aos metadados estáticos (TTL do token de autenticação, TTL do token de autorização e ID do dispositivo) anteriormente disponíveis na autenticação da Adobe Primetime.

## Exemplos {#example-mvpd-user-metadata-exch}

### Controle parental {#example-parental-control}

Este exemplo mostra a troca dos seguintes itens:

* [Programador para Troca de Metadados MVPD](#progr-mvpd-metadata-exch)

* [Fluxo de troca de metadados do MVPD para o programador](#mvpd-progr-exchange-flow)

### Programador para Troca de Metadados MVPD {#progr-mvpd-metadata-exch}

Atualmente, a API do programador, a autenticação do Adobe Primetime e os Autorizadores do MVPD suportam apenas a autorização no nível do canal. O canal é especificado como uma sequência de texto simples na chamada da API getAuthorization() do Programador. Essa string é propagada até o back-end de autorização do MVPD:

No aplicativo ou no site do Programador, o usuário escolhe um MVPD compatível com XACML (neste exemplo, &quot;TNT&quot;). Para obter informações sobre XACML, consulte [Linguagem de Marcação de Controle de Acesso eXtensible](https://en.wikipedia.org/wiki/XACML){target=_blank}.
O aplicativo do Programador forma uma solicitação AuthZ que inclui o recurso e seus metadados.  Este exemplo inclui uma classificação MPAA de &quot;pg&quot; no atributo de mídia do elemento do canal:

```XML
var resource = '<rss version="2.0" xmlns:media="http://video.search.yahoo.com/mrss/">
                    <channel> 
                        <title>TNT</title> 
                        <media:rating scheme="urn:mpaa">pg</media:rating>
                    </channel>
                </rss>';
getAuthorization(resource);
```

Na verdade, a autenticação da Adobe Primetime oferece suporte a uma autorização mais granular, até o nível de ativo, quando compatível com o MVPD e o Programador. O recurso e seus metadados são opacos no Adobe; a intenção é estabelecer um formato padrão para especificar a ID do recurso e os metadados de forma normalizada, para enviar IDs de recursos para MVPDs diferentes.

>[!NOTE]
>
>Se o usuário escolher um MVPD compatível somente com canal, a autenticação da Adobe Primetime extrai SOMENTE o título do canal (&quot;TNT&quot; no exemplo acima) e transmite somente o título para o MVPD.

### Fluxo de troca de metadados do MVPD para o programador {#mvpd-progr-exchange-flow}

A autenticação da Adobe Primetime faz as seguintes suposições:

* O MVPD envia a classificação máxima como parte da resposta SAML
* Essas informações são salvas como parte do token de autenticação
* Uma API é fornecida pela autenticação da Adobe Primetime para permitir que os Programadores recuperem essas informações
* Os programadores implementam esse recurso em seu site ou aplicativo (por exemplo, para ocultar vídeos que estão acima da classificação máxima do usuário)

```XML
<saml:Assertion ID="pfxec5f92e0-8589-3fc3-c708-f4fb8e2fad59"
                 IssueInstant="2010-07-20T10:05:41Z" Version="2.0"
                 xmlns:xs="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:AttributeStatement>
        <saml:Attribute
                Name="MaxTVRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">tv-ma</saml:AttributeValue>
        </saml:Attribute>
        <saml:Attribute
                Name="MaxMovieRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">nc-17</saml:AttributeValue>
        </saml:Attribute>
    </saml:AttributeStatement>
</saml:Assertion>
```

### Notas {#notes-mvpd-progr-metadata-exch-flow}

**Normalização e validação de recursos.** Os IDs de recurso podem ser passados como uma string simples ou uma string MRSS. Um Programador pode decidir usar o formato de string simples ou o MRSS, mas precisará de um acordo prévio com o MVPD para que o MVPD saiba como tratar esse recurso.

**Identificação do recurso e especificação de metadados** A autenticação da Adobe Primetime usa o padrão RSS com a extensão RSS do Media para especificar um recurso e seus metadados. Em conjunto com a extensão RSS do Media, a autenticação da Adobe Primetime é compatível com uma grande variedade de metadados, como controles dos pais (por meio de `<media:rating>`) ou geolocalização (`<media:location>`).

A autenticação da Adobe Primetime também pode suportar conversão transparente da sequência de canal herdada para o recurso RSS correspondente para MVPDs que exigem RSS. Na outra direção, a autenticação do Adobe Primetime suporta conversão de RSS+MRSS para título de canal simples, para MVPDs somente de canal.

**A autenticação da Adobe Primetime garante a compatibilidade total com versões anteriores das integrações existentes.** Ou seja, para Programadores que usam autenticação de nível de canal, a autenticação da Adobe Primetime tem o cuidado de empacotar a ID do canal no formato necessário antes de enviá-la para um MVPD que entende esse formato. O inverso também se aplica: se um Programador especificar todos os seus recursos em um novo formato, a autenticação da Adobe Primetime converterá o novo formato em uma sequência de caracteres de canal simples se estiver autorizando em relação a um MVPD que só faz a autorização no nível do canal.

## Casos de uso de metadados do usuário {#user-metadata-use-cases}

Os casos de uso estão mudando e se expandindo a medida que mais MVPDs fazem acordos legais e adicionam funcionalidade. A seguir estão exemplos de para que os metadados do usuário podem ser usados.

* [ID de usuário do MVPD](#mvpd-user-id)
* [ID da família](#household-user-id)
* [Código Postal](#zip-code)
* [Classificação máx (controle parental)](#max-rating-parental-control)
* [Lineup de canal](#channel-line-up)

### ID de usuário do MVPD {#mvpd-user-id}

* Conforme fornecido pelo MVPD
* Não as informações de login reais do usuário, pois estão com hash pelo MVPD
* Pode ser usado para indicar problemas com ou para usuários específicos
* Criptografado
* Suporte a MVPD: Todos os MVPDs

### ID de Usuário Doméstico {#household-user-id}

* Permite obter boas informações de métricas
* Criptografado
* Suporte a MVPD: Alguns MVPDs

### Código Postal {#zip-code}

* O CEP de faturamento do usuário
* Usada principalmente para aplicar as regras do período de congelamento de eventos esportivos
* Pode ser fornecido com a resposta AuthZ para atualizações rápidas
* Suporte a MVPD: Alguns MVPDs

### Classificação máx (controle parental) {#max-rating-parental-control}

* Inicialmente, AuthN, mais atualização de AuthZ
* Filtrar o conteúdo da interface do usuário
* MPAA ou classificações VChip
* Suporte a MVPD: Alguns MVPDs

### Lineup de canal {#channel-line-up}

* Os MVPDs podem fornecer uma lista de canais que o usuário tem direito a visualizar
* Permite uma pintura rápida da interface do usuário
* A especificação OLCA permite isso como um AttributeStatement na resposta AuthN
* MVPDs de suporte: Alguns MVPDs

<!--
>[!RELATEDINFORMATION]
>
>* [Proxy MVPD Web Service](/help/authentication/proxy-mvpd-webserv.md)
>* [Content Metadata Exhange](/help/authentication/mvpd-content-metadata-exchange.md)
>* [OLCA AuthN / AuthZ Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank}
>* [User Metadata (Programmer Integration Guide)](/help/authentication/user-metadata-feature.md)
-->
