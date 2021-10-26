---
title: API de relatórios
description: API de relatório de Auditude
source-git-commit: 7f958c83a4dd481221feb4a266440b920ac7d195
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---


# API de relatórios {#report-api}

A interface do usuário gerenciou funções para clientes e para a equipe de ativação (Adobe). Os clientes podem acessar o portal e, em seguida, criar e editar suas configurações. Eles também podem ver os relatórios de suas impressões de anúncios na interface do usuário.

As APIs funcionam nos bastidores para facilitar a comunicação dos clientes e administradores com a infraestrutura de back-end.

## Ponto de extremidade da API {#report-api-endpoint}

### Produção {#production}

`https://dai-primetime.adobe.io/report`

### Sandbox {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## Parâmetros de consulta


| Nome | Significância | Tipo de valor | Obrigatório? | Valor padrão | Restrições | Exemplo/ Valores de amostra válidos |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | Data final para os dados do relatório | data | Y | NENHUM | não mais recente do que ontem no UTC-8 | ######## |
| filtros | filtrar em uma ou mais colunas | string | N | NENHUM | ad_config_id , zone_id | ad_config_id=990.900;state=ative |
|  |  |  |  |  | Quando metaData é definida como &#39;true&#39; na solicitação, você também pode filtrar por nome. |  |
|  |  |  |  |  |  | Várias chaves de filtro são separadas por ponto e vírgula. |
|  |  |  |  |  |  | Usar valores separados por vírgula para fornecer uma lista de valores para a chave de filtro |
| groupBy | Agrupe por hora (ano \| mês \| dia) ou ad_config_id. Adconfig é sinônimo de AdRule. | string | N | NENHUM | y \| m \| d , ad_config_id | m , ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | Para groupBy no momento, forneça um de y ou m ou d |
|  |  |  |  |  |  |  |



## Cabeçalhos {#headers}

| Nome | Tipo de valor | Obrigatório | Valor de exemplo | Significância |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| Aceitar | string | Y | text/csv para CSV | Tipo de resposta esperada da API |
|  |  |  | application/json ou &#39;*/*&#39; para JSON |  |
| Token de autorização | string | Y | xyz | token de autorização |
| x-api-key | string | Y | xyz | Chave da API |
| x-gw-ims-org-id | string | Y | xyz12345 | ID da organização IMS da sua conta |

* Você pode gerar o token de autorização (também conhecido como token de acesso) seguindo as etapas detalhadas na página de ajuda da autenticação JWT do Adobe.io.
   >[!NOTE]
   >O token de autorização tem uma expiração de 24 horas, portanto, se estiver usando a API de relatório com um script recorrente, certifique-se de gerar o token de autenticação antes de sua expiração ou quando receber um erro Oauth sobre o token não ser válido.

* Para definir os valores corretos no cabeçalho da solicitação e gerar o token de autorização (usando a autenticação JWT), você precisará saber as configurações abaixo para sua conta. Entre em contato com a equipe de suporte do Primetime para obter esses valores.
ID da conta técnica

   * ID da Org
   * Api_key
   * Client_secret

## Saída {#output}

O resultado da consulta da API de relatório por padrão está no formato JSON, que especifica impressões em relação aos diferentes valores das dimensões (parâmetro groupby) solicitadas. O resultado da amostra é apresentado abaixo:

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

## Códigos e sequências de erro {#error-codes-strings}

### Formato de resposta de erro {#error-response-format}

Erro ao processar &#39;código&#39; da macro: Valor inválido especificado para o parâmetro `com.atlassian.confluence.ext.code.render.InvalidValueException`

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
| 5001010 | Ocorreu um erro interno. |
| 4001011 | As datas não são enviadas no formato necessário. |
| 4001012 | As datas estão fora do intervalo. |
| 4001013 | Parâmetro obrigatório ausente. |
| 4001014 | A lista de zonas está vazia para a conta. |
| 4001015 | Chaves de filtro inválidas na solicitação. |
| 4001016 | Opção GroupBy inválida na solicitação. |
| 4001017 | ID inválida fornecida na solicitação |

## Exemplos de chamadas e resultados esperados {#sample-calls-expected-results}

A seguir, o comando curl para obter contagens mensais de impressões entre 2020-07-01 e 2021-06-30 usando o token de acesso:

**Exemplo de chamada da API de relatório**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| Exemplo de chamada/caso de uso | Resultado esperado |
|---|---|
| Buscar relatório com o GET de datas de início e término: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01 cabeçalho : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a esta conta total_impressões |
| Buscar relatório com GroupBy = d \| m \| y GET: [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y header : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a essas datas de conta (mm-dd-yyyy \| mm-aaaa em formato \| aaaa) total_impressões |
| Buscar relatório com o GET GroupBy = ad_config_id: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id header : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a esta conta ad_config_id total_impressions |
| Buscar relatório com GroupBy = d \| m \| y e GET ad_config_id: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id header : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a esta conta e datas ad_config_id (mm-dd-yyyy \| mm-aaaa formato \| aaaa) total_impressões |
| Buscar relatório com metaData=true e groupBy=d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id header : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a esta conta ad_config_id nome total_impressões |
| Buscar relatório com groupBy=d \| m \| y e GET ad_config_id: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,ad_config_id header : Accept = application/json. ou */* | Json com os seguintes parâmetros com todos os anúncios pertencentes a esta conta e o nome_config_id total_impressões datas (mm-dd-aaaa \| mm-aaaa \| formato aaaa) |
| Buscar relatório para obter todas as linhas para um determinado intervalo de datas (com não paginado = true) GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 31 entradas na matriz Json retornada |
| Buscar relatório com o GET de parâmetros de consulta de página válidos: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 5 entradas na matriz retornada |
| Buscar relatório, com o GET de formato csv: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 cabeçalho : Accept = text/csv | A string CSV é retornada, com cabeçalho: total_impressões |
| Buscar relatório, com formato csv , e groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y header : Accept = text/csv | A string CSV é retornada, com cabeçalho: total_impressões datas (mm-dd-yyyy \| mm-yyyy \| formato aaaa) |
| Buscar relatório, com formato csv , e metadados = GET verdadeiro: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true header : Accept = text/csv | A string CSV é retornada, com cabeçalho: total_impressões |
| Buscar relatório, com formato csv , metadados = true e groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y header : Accept = text/csv | A string CSV é retornada, com cabeçalho: total_impressões datas (mm-dd-yyyy \| mm-yyyy \| formato aaaa) |


## Política de limitação da API de relatório {#report-api-throttling-policy}

* 5 As solicitações de API são permitidas durante uma janela de 5 segundos para cada usuário.
* Se um usuário ultrapassar o limite, a resposta será atrasada em 5 segundos.
* Se um usuário fizer mais de 10 chamadas dentro de uma janela de 5 segundos, ele começará a ser rejeitado com a resposta &quot;429 Demasiadas solicitações&quot;.
