---
title: Benefícios do uso do parâmetro deviceType sem cliente nas métricas de autenticação do Primetime
description: Benefícios do uso do parâmetro deviceType sem cliente nas métricas de autenticação do Primetime
exl-id: a5004887-d5fa-468e-971b-10806519175b
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# Benefícios do uso do parâmetro deviceType sem cliente nas métricas de autenticação do Primetime {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

</br>

## Contexto

Embora opcional, o parâmetro `deviceType` da API sem cliente, quando presente, é usada nas métricas de autenticação do Primetime que estão sendo expostas por meio de [Monitoramento do Serviço de Qualificação](/help/authentication/entitlement-service-monitoring-overview.md).

Tendo em conta que a ligação entre a `deviceType` e seu **benefícios** se as métricas de autenticação do Primetime não foram inicialmente declaradas, o escopo dessa nota técnica é adicionar mais informações sobre elas.

## Explicação

A variável `deviceType` O parâmetro estava presente na API sem cliente desde a primeira versão, mas suas implicações nas métricas de autenticação do Primetime foram adicionadas em uma versão mais recente.



>[!IMPORTANT]
>
>Se o parâmetro `deviceType` estiver definido corretamente, isso significa que ele tem o seguinte **benefício** no Monitoramento do serviço de qualificação: ele oferece métricas que são [detalhado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) ao usar sem cliente, para que diferentes tipos de análise possam ser executados para, por exemplo, Roku, Apple TV, Xbox etc.


Para obter mais informações sobre a API de monitoramento do serviço de qualificação, consulte a [árvore de drill-down,](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) que ilustra a [dimensões](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) disponíveis no ESM 2.0.

>[!NOTE]
>
>O conteúdo desta nota técnica também foi adicionado à [API sem cliente](#clientless_device_type).




## Implementação

Para se beneficiar totalmente das métricas de autenticação do Primetime, há dois tipos de [APIs sem cliente](#web_srvs_summary) que estão sendo utilizadas e que precisam ter a configuração `deviceType` definir:

1. APIs que têm `regcode` como parâmetro obrigatório e usará o parâmetro `deviceType` parâmetro que foi definido ao criar o `regcode`, com a seguinte chamada de API:
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggie/v1/{requestorId}/regcode](#reg_serv)

1. APIs que têm o `deviceType` como parâmetro opcional:
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorize](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediatoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preauthorize](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

Nossa recomendação é usar o `deviceType` e transmita o tipo de dispositivo sem cliente correto para todas as APIs.
