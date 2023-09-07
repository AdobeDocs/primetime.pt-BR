---
title: Metadados do usuário
description: Metadados do usuário
exl-id: 3d7b6429-972f-4ccb-80fd-a99870a02f65
source-git-commit: 4479df7985da16e8632a538f1042de05109f2392
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Metadados do usuário {#user-metadata}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Endpoints da REST API {#clientless-endpoints}

`<REGGIE_FQDN>`:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

`<SP_FQDN>`:

* Produção - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Estágios - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Descrição {#description}

Recupere os metadados que o MVPD compartilhou sobre o usuário autenticado.


| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>`/api/v1/tokens/usermetadata | Aplicativo de transmissão</br></br>ou</br></br>Serviço de programador | 1. requerente</br>2.  deviceId (Obrigatório)</br>3.  device_info/X-Device-Info (Obrigatório)</br>4.  deviceType</br>5.  deviceUser (obsoleto)</br>6.  appId (obsoleto) | GET | XML ou JSON que contém metadados do usuário ou detalhes do erro, se malsucedido. | 200 - Sucesso<p>404 - Nenhum metadado encontrado<p>412 - Token de autenticação inválido (por exemplo, token expirado) |


| Parâmetro de entrada | Descrição |
| --- | --- |
| solicitante | O requestorId do Programador para o qual esta operação é válida. |
| deviceId | Os bytes de id do dispositivo. |
| device_info/<p>X-Device-Info | Informações do dispositivo de transmissão.<p>**Nota**: isso PODE ser passado para device_info como um parâmetro de URL, mas devido ao tamanho potencial desse parâmetro e às limitações no comprimento de um URL do GET, ele DEVE ser passado como X-Device-Info no cabeçalho http. </br></br>Veja todos os detalhes em **Transmitindo Informações sobre Dispositivo e Conexão** <!--http://tve.helpdocsonline.com/passing-device-information-->. |
| _deviceType_ | O tipo de dispositivo (por exemplo, Roku, PC).<p>Se esse parâmetro estiver definido corretamente, o ESM oferecerá métricas que são [detalhado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#progr-filter-metrics) ao usar sem cliente, para que diferentes tipos de análise possam ser executados para, por exemplo, Roku, Apple TV, Xbox etc.<p>Consulte [Benefícios do uso do parâmetro de tipo de dispositivo sem cliente nas métricas Pass](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)<p>**Nota:** A variável `device_info` O substitui esse parâmetro. |
| _deviceUser_ | O identificador do usuário do dispositivo.</br></br>**Observação:**se usado, `deviceUser` deve ter os mesmos valores que no [Criar código de registro](/help/authentication/registration-code-request.md) solicitação. |
| _appId_ | O id/nome do aplicativo. <p>**Nota:**A `device_info` O substitui esse parâmetro. Se usado, `appId` deve ter os mesmos valores que no **Criar código de registro** solicitação. |

>[!NOTE]
> 
>As informações de metadados do usuário devem estar disponíveis após a conclusão do fluxo de autenticação, mas podem ser atualizadas no fluxo de autorização, dependendo do MVPD e do tipo de metadados.




## Exemplo de resposta {#sample-response}

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
    }
```

Na raiz do objeto, haverá três nós:

* **atualizado**: especifica um carimbo de data e hora UNIX que representa a última vez que os metadados foram atualizados. Essa propriedade será definida inicialmente pelo servidor ao gerar os metadados durante a fase de autenticação. Chamadas subsequentes (após a atualização dos metadados) resultarão em um carimbo de data e hora incrementado.
* **dados**: contém os valores reais de metadados.
* **criptografado**: uma matriz que lista as propriedades criptografadas. Para descriptografar um valor de metadados específico, o Programador deve executar uma decodificação Base64 nos metadados e, em seguida, aplicar uma descriptografia RSA no valor resultante, usando sua própria chave privada (o Adobe criptografa os metadados no servidor usando o certificado público do Programador).

No caso de um erro, o servidor retornará um objeto XML ou JSON que especifica uma mensagem de erro detalhada.

Para obter mais informações, consulte [Metadados do usuário](/help/authentication/user-metadata-feature.md).

[Voltar para Referência da API REST](/help/authentication/rest-api-reference.md)
