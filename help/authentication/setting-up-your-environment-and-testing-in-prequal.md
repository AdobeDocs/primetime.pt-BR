---
title: Configuração do ambiente e teste na pré-qualificação
description: Configuração do ambiente e teste na pré-qualificação
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Configuração do ambiente e teste em qual{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>A conteúdo neste página é fornecida somente para fins de informação. O uso desta API exige uma licença atual da Adobe Systems. Não é permitido usar uso não autorizado.

O objetivo desta nota técnica é ajudar nossos parceiros a configurar seus ambiente e start testar um novo build implantado no ambiente Adobe Systems de qualificação.

Como há dois build tipos: ***produção*** e ***preparação*** , neste documento iremos focalizar na configuração de produção com a menção de que todas as etapas são as mesmas para a preparação, somente as URLs são diferentes.

As etapas 1 e 2 estão Configurando o teste ambiente em uma das máquinas de teste, a etapa 3 é a verificação do fluxo básico e as etapas 4 &amp; 5 estão apresentando algumas diretrizes de teste.

>[!IMPORTANT]
>
> É muito importante executar as etapas 1 e 2 cada vez que você quiser alterar sua ambiente de teste (mudar do preparo para o perfil de produção ou da outra maneira)


## ETAPA 1. Resolução de Passagem de domínio para um IP {#resolving-pass-domain-to-an-ip}

* Para localizar um IP do balanceador de carga que possa ser usado para falsificação, execute o seguinte comando:

* **No Windows**

  ```cmd
  C:\>nslookup sp-prequal.auth.adobe.com
  ...
  Addresses:  52.13.71.11
              54.184.208.150
  ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **No Linux/Mac**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>Domínios excluídos da resposta porque não são relevantes e podem diferir de usuário para usuário.

>[!IMPORTANT]
>
> Esses endereços IP podem mudar no futuro e podem não ser os mesmos para usuários em regiões geográficas diferentes.


## ETAPA 2.  Simulação da ambiente de pré qualificação para ser produção {#spoofing-the-prequalification-environment}

* Editar o arquivo C:\\windows\\System32\\drivers\\etc\\hosts *(no Windows) ou* o *arquivo/etc/hosts* (no Macintosh/Linux/Android) e adicione o seguinte:

* perfil de produção de spoof
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Falsificação no Android:** Para falsificar no Android, você precisa usar um emulador de Android.

* Quando a falsificação estiver em vigor, você poderá simplesmente usar os URLs comuns para os perfis de produção e preparo: (ou seja, `http://sp.auth-staging.adobe.com` e `http://entitlement.auth-staging.adobe.com` e você chegará ao botão *ambiente/produção de pré-qualificação* da* nova build.


## ETAPA 3.  Verifique se você está apontando para o ambiente correto {#Verify-you-are-pointing-to-the-right-environment}

**Essa é uma etapa fácil:**

* Carregue [ o direito de prequal ambiente ](https://entitlement-prequal.auth.adobe.com/environment.html) e [ qualificação ](https://entitlement.auth.adobe.com/environment.html) . Eles devem retornar a mesma resposta.


## ETAPA 4.  Executar um fluxo de autenticação/autorização simples usando o site do programador {#peform-a-simple-auth-flow}

* Esta etapa exige o endereço do site do programador e algumas credenciais MVPD válidas (um usuário que é autenticado e autorizado).

## ETAPA 5.  Execute testes de cenário usando os sites do programador {#perform-scenario-testing-using-programmer-website}

* Depois de concluir a configuração do ambiente e garantir que o fluxo de autenticação básica-autorização esteja funcionando, você pode prosseguir com o teste de cenários mais complexos.


## ETAPA 6.  Realizar testes usando o site de teste da API {#perform-testing-using-api-testing-site}

* Se quiser aprofundar no teste da autenticação do Adobe Primetime, recomendamos que você use o [Site de teste da API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Você pode encontrar mais detalhes no site de teste da API em [Como testar fluxos de autenticação e autorização usando o site de teste da API do Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).
