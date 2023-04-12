---
title: Metadados do usuário
description: Metadados do usuário
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# Metadados do usuário {#user-metadata}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Endpoints REST API {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descrição {#description}

Recupere os metadados que o MVPD compartilhou sobre o usuário autenticado.

<div>


| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/usermetadata | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. solicitante</br>2.  deviceId (Obrigatório)</br>3.  device_info/X-Device-Info (Obrigatório)</br>4.  deviceType</br>5.  deviceUser (obsoleto)</br>6.  appId (obsoleto) | GET | XML ou JSON contendo metadados do usuário ou detalhes do erro, se não tiver êxito. | 200 - Sucesso</br></br>404 - Nenhum metadados encontrado</br></br>412 - Token AuthN inválido (por exemplo, token expirado) |


| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O ID do solicitador do Programador para o qual esta operação é válida. |
| deviceId | Os bytes da ID do dispositivo. |
| device_info/</br></br>X-Device-Info | Informações do dispositivo de transmissão.</br></br>**Observação**: Isso PODE ser passado device_info como um parâmetro de URL, mas devido ao tamanho potencial desse parâmetro e limitações no comprimento de um URL de GET, ele deve ser passado como X-Device-Info no cabeçalho http. </br></br>Veja os detalhes completos em **Transmitindo informações de dispositivo e conexão** <!--http://tve.helpdocsonline.com/passing-device-information-->. |
| _deviceType_ | O tipo de dispositivo (por exemplo, Roku, PC).</br></br>Se esse parâmetro for definido corretamente, o ESM oferece métricas que são [detalhado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#progr-filter-metrics) ao usar a opção sem cliente, para que diferentes tipos de análise possam ser executados para, por exemplo, Roku, AppleTV, Xbox etc.</br></br>Consulte [Benefícios do uso do parâmetro de tipo de dispositivo sem cliente em Métricas de passagem ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Observação:** O `device_info` substitui esse parâmetro. </br> |
| _deviceUser_ | O identificador do usuário do dispositivo.</br></br>**Observação:**se usado, `deviceUser` deve ter os mesmos valores de [Criar código de registro](/help/authentication/registration-code-request.md) solicitação. |
| _appId_ | A ID/nome do aplicativo. </br></br>**Observação:**A variável `device_info` substitui esse parâmetro. Se usado, `appId` deve ter os mesmos valores de **Criar código de registro** solicitação. |

>[!NOTE]
> 
>As informações de metadados do usuário devem estar disponíveis após a conclusão do fluxo de autenticação, mas podem ser atualizadas no fluxo de autorização, dependendo do MVPD e do tipo de metadados.

</br>

## Resposta de exemplo {#sample-response}

Após uma chamada bem-sucedida, o servidor responderá com um objeto XML (padrão) ou JSON com uma estrutura semelhante à apresentada abaixo:

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
              zip: ["12345", "34567"],
              maxRating: { 
                  "MPAA": "PG-13",
                  "VCHIP": "TV-Y", 
                  "URL": "http://exam.pl/e/manage/ratings"
              },
              householdID: "3456",
              userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
              channelID: ["channel-1", "channel-2"]
    }
```

Na raiz do objeto, haverá três nós:

* **atualizado**: especifica um carimbo de data e hora UNIX que representa a última vez que os metadados foram atualizados. Essa propriedade será definida inicialmente pelo servidor ao gerar os metadados durante a fase de autenticação. As chamadas subsequentes (após a atualização dos metadados) resultarão em um aumento no carimbo de data e hora.

* **dados**: contém os valores de metadados reais.

* **criptografado**: uma matriz que lista as propriedades criptografadas. Para descriptografar um valor de metadados específico, o Programador deve executar um decodificador Base64 nos metadados e aplicar uma descriptografia RSA no valor resultante, usando sua própria chave privada (o Adobe criptografa os metadados no servidor usando o certificado público do Programador).

No caso de um erro, o servidor retornará um objeto XML ou JSON que especifica uma mensagem de erro detalhada.

Para obter mais informações, consulte [Metadados do usuário](/help/authentication/user-metadata.md).

### [Voltar para Referência da API REST](/help/authentication/rest-api-reference.md).
