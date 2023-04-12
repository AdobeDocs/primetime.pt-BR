---
title: Como configurar seu ambiente e testar no Pre-Qual
description: Como configurar seu ambiente e testar no Pre-Qual
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Como configurar seu ambiente e testar no Pre-Qual{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

O objetivo dessa nota técnica é ajudar nossos parceiros a configurar seu ambiente e começar a testar uma nova build implantada no ambiente de pré-qualificação do Adobe.

Como há dois sabores de construção: ***produção*** e ***preparo***, neste documento, vamos nos concentrar na configuração de produção com a menção de que todas as etapas são as mesmas para preparo, apenas os URLs são diferentes.

As etapas 1 e 2 estão configurando o ambiente de teste em uma das máquinas de teste, a etapa 3 é uma verificação do fluxo básico e as etapas 4 e 5 estão apresentando algumas diretrizes de teste.

>[!IMPORTANT]
>
> É muito importante executar as etapas 1 e 2 sempre que quiser alterar o ambiente de teste (alternar do perfil de preparo para o de produção ou o contrário)
 

## ETAPA 1. Resolvendo o domínio passar para um IP {#resolving-pass-domain-to-an-ip}

* Para localizar um IP de balanceador de carga que possa ser usado para falsificação, execute o seguinte comando:

* **No Windows**

   ```cmd
   C:\>nslookup sp-prequal.auth.adobe.com
   ...
   Addresses:  52.13.71.11
               54.184.208.150
   ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **No Linux/Mac**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>Os domínios excluídos da resposta, pois não são relevantes e podem ser diferentes de usuário para usuário.

>[!IMPORTANT]
>
> Esses endereços IP podem mudar no futuro e podem não ser os mesmos para usuários em diferentes regiões geográficas.


## ETAPA 2.  Detecção do ambiente de pré-qualificação para produção {#spoofing-the-prequalification-environment}

* Edite o *c:\\windows\\System32\\drivers\\etc\\hosts* arquivo (no Windows) ou */etc/hosts* (no Macintosh/Linux/Android) e adicione o seguinte:

* Perfil de produção do Spot
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Spoofing no Android:** Para evitar problemas no Android, é necessário usar um emulador de Android.

* Quando a falsificação estiver em vigor, você poderá simplesmente usar os URLs regulares para os perfis de produção e de preparo: (ou seja, `http://sp.auth-staging.adobe.com` e `http://entitlement.auth-staging.adobe.com` e você realmente acertará no *ambiente/produção de pré-qualificação* da nova build*.


## ETAPA 3.  Verifique se você está apontando para o ambiente certo {#Verify-you-are-pointing-to-the-right-environment}

**Esta é uma etapa fácil:**

* load [ambiente de preigualdade de direitos](https://entitlement-prequal.auth.adobe.com/environment.html) e [direito](https://entitlement.auth.adobe.com/environment.html). Eles devem retornar a mesma resposta.


## ETAPA 4.  Execute um fluxo de autenticação/autorização simples usando o site do programador {#peform-a-simple-auth-flow}

* Esta etapa requer o endereço do site do programador e algumas credenciais válidas do MVPD (um usuário que está autenticado e autorizado).

## ETAPA 5.  Realize testes de cenário usando os sites do programador {#perform-scenario-testing-using-programmer-website}

* Após concluir a configuração do ambiente e garantir que o fluxo básico de autenticação-autorização está funcionando, você pode continuar com o teste de cenários mais complexos.


## ETAPA 6.  Realize testes usando o site de teste da API {#perform-testing-using-api-testing-site}

* Se você quiser aprofundar os testes de autenticação da Adobe Primetime, recomendamos que você use a variável [Site de teste da API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Você pode encontrar mais detalhes sobre o site de teste da API em [Como testar os fluxos de Autenticação e Autorização usando o site de teste API do Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

