---
title: Monitoramento da autenticação da Adobe Primetime
description: Monitoramento da autenticação da Adobe Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Monitoramento da autenticação da Adobe Primetime {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#intro}

Os clientes podem usar [Nagios](http://www.nagios.org) ou outras ferramentas para verificar se a autenticação da Adobe Primetime está ativa ou inativa. 

## Monitorar pontos de extremidade {#monitoring-endpoints}

### Endpoints que você pode monitorar {#endpoints-to-monitor}

* O endpoint de configuração para todas as plataformas: `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]`- Ele está disponível por HTTP ou HTTPS (dependendo da escolha feita pelo desenvolvedor do provedor de conteúdo). Se esse terminal estiver ausente, significa que o conteúdo não estará disponível em todas as plataformas e em todos os MVPDs. Para a API REST sem cliente, também temos o seguinte terminal:  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

* Os seguintes endpoints fazem parte do SDK da Web de autenticação da Adobe Primetime.  Se estiver faltando, significa que o pay-TVpass está desativado para todos os programadores e todas as propriedades da Web:

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`

 
### Endpoints que você não deve monitorar {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

   Você sempre receberá um erro 503, pois esse terminal precisa de uma resposta MVPD SAML.

* Outros pontos de extremidade de direito - `adobe-services/1.0/authenticate/`, `adobe-services/1.0/deviceShortAuthorize`, `adobe-services/1.0/authorize`

Não é possível monitorar esses endpoints porque eles precisam de uma carga para uma resposta relevante.
