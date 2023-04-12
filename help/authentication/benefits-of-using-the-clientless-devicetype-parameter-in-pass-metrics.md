---
title: Benefícios do uso do parâmetro ClientType nas métricas de autenticação do Primetime
description: Benefícios do uso do parâmetro ClientType nas métricas de autenticação do Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# Benefícios do uso do parâmetro ClientType nas métricas de autenticação do Primetime {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

## Contexto

Embora seja opcional, o parâmetro `deviceType` da API sem cliente, quando presente, é usada em métricas de autenticação do Primetime que estão sendo expostas por meio de [Monitoramento do serviço de direito](/help/authentication/entitlement-service-monitoring-overview.md).

Considerando que a ligação entre a `deviceType` e seu **benefícios** no Primetime authentication metrics não foi declarado inicialmente, o escopo dessa nota técnica é adicionar mais informações sobre elas.

## Explicação

O `deviceType` estava presente na API sem cliente desde a primeira versão, mas suas implicações nas métricas de autenticação do Primetime foram adicionadas em uma versão mais recente.



>[!IMPORTANT]
>
>Se o parâmetro `deviceType` está definida corretamente e tem o seguinte **benefício** em Monitoramento do Serviço de Direitos: ele oferece métricas que são [detalhado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) ao usar a opção sem cliente, para que diferentes tipos de análise possam ser executados para, por exemplo, Roku, AppleTV, Xbox etc.


Para obter mais informações sobre a API de monitoramento do serviço de direito, consulte [árvore de detalhamento,](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) que ilustra a [dimensões](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) (recursos) disponível no ESM 2.0.

>[!NOTE]
>
>O conteúdo dessa nota técnica também foi adicionado ao [API sem cliente](#clientless_device_type).




## Implementação

Para se beneficiar totalmente das métricas de autenticação do Primetime, há dois tipos de [APIs sem cliente](#web_srvs_summary) que estão sendo usadas e que precisam ter o `deviceType` definido:

1. APIs que têm `regcode` como um parâmetro obrigatório e usará o `deviceType` parâmetro que foi definido ao criar o `regcode`, com a seguinte chamada de API:
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggie/v1/{requestorId}/regcode](#reg_serv)

1. APIs que têm o `deviceType` como parâmetro opcional:
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorized](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediatoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/pré-autorizar](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

Nossa recomendação é usar a variável `deviceType` e transmita o tipo de dispositivo sem cliente correto para todas as APIs.


