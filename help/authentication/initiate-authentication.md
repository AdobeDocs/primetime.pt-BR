---
title: Iniciar Autenticação
description: Iniciar autenticação
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Iniciar Autenticação {#initiate-authentication}

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

Inicia o processo de autenticação informando um evento de seleção MVPD. Cria um registro no banco de dados de autenticação do Primetime, que é reconciliado quando uma resposta bem-sucedida é recebida do MVPD. 



| Endpoint | Chamado  </br>Por | Entrada   </br>Params | HTTP  </br>Método | Resposta | HTTP  </br>Resposta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authentication | Módulo AuthN | 1. requestor_id (Obrigatório)</br>2.  mso_id (Obrigatório)</br>3.  reg_code (Obrigatório)</br>4.  domain_name (Obrigatório)</br>5.  noflash=true -  </br>    (Obrigatório, parâmetro Residual)</br>6.  no_iframe=true (Obrigatório, parâmetro Residual)</br>7.  parâmetros adicionais (Opcional)</br>8.  redirect_url (Obrigatório) | GET | O Aplicativo Web de Logon é redirecionado para a página de logon do MVPD. | 302 para implementações completas de redirecionamento |

{style="table-layout:auto"}


| Parâmetro de entrada | Descrição |
| --- | --- |
| requestor_id | O solicitante do Programador para o qual esta operação é válida. |
| mso_id | A ID MVPD para a qual esta operação é válida. |
| reg_code | O código de registro gerado pelo serviço Reggie. |
| nome_do_domínio | O domínio de origem. |
| redirect_url | O url de redirecionamento do aplicativo Web de logon após a conclusão da autenticação. |

{style="table-layout:auto"}

</br>

>[!IMPORTANT]
> 
>**Importante: Parâmetros obrigatórios -** Independentemente da implementação no lado do cliente, todos os parâmetros acima são obrigatórios.
>
>
>Exemplo:    
>
>
```
>domain_name=loginwebapp.com
>mso_id=sampleMvpdId
>reg_code=RO0885W
>requestor_id=sampleRequestorId
>noflash=true
>redirect_url=http://loginwebapp.com
>```

>[!IMPORTANT]
> 
>**Importante: Parâmetros opcionais**
>
>A chamada também pode conter parâmetros opcionais que permitem outras funcionalidades como:
>
> * generic\_data - permite o uso de [TempPass Promocionais](/help/authentication/promotional-temp-pass.md)
>
>```JSON
>Example:
>   generic_data=("email":"email@domain.com")
>```


### **Notas** {#notes}

* O valor da variável `domain_name` deve ser definido como um dos nomes de domínio registrados com a autenticação do Primetime. Para obter mais detalhes, consulte [Registro e inicialização](/help/authentication/programmer-overview.md).

* [Evite usar &#39;&amp;&#39;reg\_code na solicitação de autenticação (Nota Técnica)](/help/authentication/clientless-avoid-using-reg-code-in-authenticate-request.md)

* O `redirect_url` deve ser o último em ordem

* O valor da variável `redirect_url` deve ser codificado por URL


