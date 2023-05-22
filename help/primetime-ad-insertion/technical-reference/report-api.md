---
title: API de relatórios
description: API de relatório de auditoria
exl-id: 50eb4869-3765-4591-8c41-794b29d50044
source-git-commit: 628544e38616715e83e0274ba26cf93302ce0e61
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---

# API de relatórios {#report-api}

A interface do usuário tem funções gerenciadas para clientes e para a equipe de ativação (Adobe). Os clientes podem acessar o portal e, em seguida, criar e editar suas configurações. Ele também pode ver os relatórios de suas impressões de anúncios na interface do usuário do.

As APIs funcionam nos bastidores para facilitar a comunicação dos clientes e administradores com a infraestrutura de back-end.

Para explorar as [!DNL Primetime Ad Insertion] APIs: consulte [Pontos de acesso da API do Ad Insertion na interface do usuário alternada](https://adconfigservice-va6.cloud.adobe.io/swagger-ui/index.html#/).

## Endpoint da API {#report-api-endpoint}

### Produção {#production}

`https://dai-primetime.adobe.io/report`

### Sandbox {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## Parâmetros de consulta


| Nome | Significância | Tipo de valor | Obrigatório? | Valor padrão | Restrições | Exemplo/ Valores válidos de exemplo |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | Data final dos dados do relatório | data | Y | NENHUM | não mais recente que ontem em UTC-8 | ######## |
| filtros | filtrar em uma ou mais colunas | string | N | NENHUM | ad_config_id , zone_id | ad_config_id=990,900;state=ativo |
|  |  |  |  |  | Quando os metadados são definidos como &quot;true&quot; na solicitação, também é possível filtrar por nome. |  |
|  |  |  |  |  |  | Várias teclas de filtro são separadas por ponto e vírgula. |
|  |  |  |  |  |  | Use valores separados por vírgula para fornecer uma lista de valores para a chave de filtro |
| groupBy | Agrupar por hora ( ano \| mês \| dia) ou ad_config_id. Adconfig é sinônimo de AdRule. | string | N | NENHUM | y \| m \| d , ad_config_id | m , ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | Para groupBy no prazo, forneça um dos valores y, m ou d |
|  |  |  |  |  |  |  |



## Cabeçalhos {#headers}

| Nome | Tipo de valor | Obrigatório | Valor de exemplo | Significância |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| Aceitar | string | Y | text/csv para CSV | Tipo de resposta esperada da API |
|  |  |  | application/json ou &quot;*/*&#39; para JSON |  |
| Token de autorização | string | Y | xyz | token de autorização |
| x-api-key | string | Y | xyz | Chave de API |
| x-gw-ims-org-id | string | Y | xyz12345 | ID da organização IMS da sua conta |

* Você pode gerar o token de autorização (também conhecido como token de acesso) seguindo as etapas detalhadas na página de ajuda da autenticação JWT do Adobe.io.
   >[!NOTE]
   >O token de autorização expira em 24 horas. Portanto, se você estiver usando a API de relatório com um script recorrente, gere o token de autenticação antes de expirar ou quando receber um erro de Oauth sobre a não validade do token.

* Para definir os valores corretos no cabeçalho da solicitação e gerar o token de autorização (usando a autenticação JWT), você precisará saber as configurações abaixo para sua conta. Entre em contato com a equipe de suporte do Primetime para obter esses valores.
ID da conta técnica

   * ID da organização
   * Api_key
   * Client_secret

## Output {#output}

O resultado da consulta da API de relatório por padrão está no formato JSON, que especifica impressões em relação aos diferentes valores das dimensões (parâmetro groupby) solicitadas. O exemplo de saída é fornecido abaixo:

```JSON
[
    {
        "dates": "07-2020",
        "total_impressions": 213007041
    },
    {
        "dates": "08-2020",
        "total_impressions": 174711626
    },
    {
        "dates": "09-2020",
        "total_impressions": 102863153
    }
]
```

## Códigos de erro e strings {#error-codes-strings}

### Formato de resposta de erro {#error-response-format}

Erro ao renderizar macro &#39;code&#39;: valor inválido especificado para o parâmetro `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

A tabela abaixo lista os códigos de erro e as mensagens que a API de relatório pode retornar. Para erros relacionados à camada de autorização, consulte a [documentação do código de erro](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) de Adobe.io.

| Código de erro | Mensagem de erro |
|-----------------------|------------------------------------------|
| 4001007 | Detalhes do usuário inválidos. |
| 4001008 | Todas as zonas não são da mesma conta. |
| 5001010 | Erro interno. |
| 4001011 | As datas não são enviadas no formato obrigatório. |
| 4001012 | As datas estão fora do intervalo. |
| 4001013 | Parâmetro obrigatório ausente. |
| 4001014 | A lista de zonas da conta está vazia. |
| 4001015 | Chaves de filtro inválidas na solicitação. |
| 4001016 | Opção GroupBy inválida na solicitação. |
| 4001017 | ID inválida fornecida na solicitação |

## Exemplos de chamadas e resultados esperados {#sample-calls-expected-results}

A seguir está o comando curl para obter contagens de impressão mensais entre 07-01-2020 e 30-06-2021 usando o token de acesso:

**Exemplo de chamada de API de relatórios**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| Exemplo de chamada/caso de uso | Resultado esperado |
|---|---|
| Buscar relatório com GET de datas de início e término: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01 cabeçalho : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a esta conta total_impressions |
| Buscar relatório com GroupBy = d \| m \| y GET: [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y cabeçalho : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a essas datas de conta (formato mm-dd-aaaa \| mm-aaaa \|) total_impressions |
| Buscar relatório com GroupBy = ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id cabeçalho : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a esta conta ad_config_id total_impressions |
| Buscar relatório com GroupBy = d \| m \| y e ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id cabeçalho : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a essa conta ad_config_id dates (formato mm-dd-aaaa \| mm-aaaa \|) total_impressions |
| Buscar relatório com metaData=true e groupBy=d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id cabeçalho : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a esta conta ad_config_id name total_impressions |
| Buscar relatório com GET groupBy=d \| m \| y e ad_config_id: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,ad_config_id cabeçalho : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a essa conta ad_config_id name total_impressions dates (formato mm-dd-aaaa \| mm-aaaa \|) |
| Busque o relatório para obter todas as linhas para um intervalo de datas especificado (com unpaged = true) GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 31 entradas na matriz Json retornada |
| Buscar relatório com parâmetros de consulta de página válidos GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 5 entradas na matriz retornada |
| Buscar relatório, com GET de formato csv: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 cabeçalho : Accept = text/csv | A cadeia de caracteres CSV é retornada, com o cabeçalho: total_impressions |
| Buscar relatório, com formato csv e groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y cabeçalho : Accept = text/csv | A cadeia de caracteres CSV é retornada com o cabeçalho: total_impressions datas (formato mm-dd-aaaa \| mm-aaaa \| aaaa) |
| Buscar relatório, com formato csv e metadados = GET verdadeiro: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true cabeçalho : Accept = text/csv | A cadeia de caracteres CSV é retornada, com o cabeçalho: total_impressions |
| Buscar relatório, com formato csv , metadados = true e groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y cabeçalho : Accept = text/csv | A cadeia de caracteres CSV é retornada com o cabeçalho: total_impressions datas (formato mm-dd-aaaa \| mm-aaaa \| aaaa) |


## Política de Limitação da API de Relatório {#report-api-throttling-policy}

* São permitidas cinco solicitações de API durante uma janela de cinco segundos para cada usuário.
* Se um usuário ultrapassar o limite, a resposta será atrasada em 5 segundos.
* Se um usuário fizer mais de 10 chamadas em uma janela de 5 segundos, ele começará a ser rejeitado com a resposta &quot;429 Demasiadas solicitações&quot;.
