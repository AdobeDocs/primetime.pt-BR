---
title: Monitoramento da autenticação do Adobe Primetime
description: Monitoramento da autenticação do Adobe Primetime
exl-id: fb000e9d-b5aa-45b1-a914-9e419ec8a4d9
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Monitoramento da autenticação do Adobe Primetime {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Introdução {#intro}

Os clientes podem usar [Nagios](http://www.nagios.org) ou outras ferramentas para verificar se a autenticação do Adobe Primetime está ativa ou inativa.

## Monitorar endpoints {#monitoring-endpoints}

### Pontos de extremidade que você pode monitorar {#endpoints-to-monitor}

* O endpoint de configuração para todas as plataformas: `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]`- Está disponível por HTTP ou HTTPS (dependendo da escolha feita pelo desenvolvedor do provedor de conteúdo). Se esse endpoint estiver ausente, significa que o conteúdo não estará disponível em todas as plataformas e todos os MVPDs. Para a API REST sem cliente, também temos o seguinte endpoint:  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

* Os endpoints a seguir fazem parte do SDK da Web de autenticação da Adobe Primetime.  Se estiver faltando, significa que o pay-TVpass está desativado para todos os programadores e todas as propriedades da web:

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`


### Endpoints que você não deve monitorar {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

  Você sempre receberá um erro 503, pois esse endpoint precisa de uma resposta SAML MVPD nele.

* Outros endpoints de direitos - `adobe-services/1.0/authenticate/`, `adobe-services/1.0/deviceShortAuthorize`, `adobe-services/1.0/authorize`

Não é possível monitorar esses pontos de extremidade porque eles precisam de uma carga para uma resposta relevante.
