---
title: Configuração do ambiente e teste na pré-qualificação
description: Configuração do ambiente e teste na pré-qualificação
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Configuração do ambiente e teste na pré-qualificação{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

O objetivo desta nota técnica é ajudar nossos parceiros a configurar seu ambiente e começar a testar uma nova build implantada no ambiente de pré-qualificação do Adobe.

Como há duas opções de build: ***produção*** e ***estágios*** No entanto, neste documento, nos concentraremos na configuração de produção com a menção de que todas as etapas são as mesmas para o preparo, somente os URLs são diferentes.

As etapas 1 e 2 estão configurando o ambiente de teste em uma das máquinas de teste. A etapa 3 é uma verificação do fluxo básico e as etapas 4 e 5 estão apresentando algumas diretrizes de teste.

>[!IMPORTANT]
>
> É muito importante executar as etapas 1 e 2 sempre que quiser alterar o ambiente de teste (alternando do ambiente de preparo para o perfil de produção ou o contrário)
 

## ETAPA 1. Resolução de Passagem de domínio para um IP {#resolving-pass-domain-to-an-ip}

* Para localizar um IP do balanceador de carga que possa ser usado para falsificação, execute o seguinte comando:

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
>Domínios excluídos da resposta porque não são relevantes e podem diferir de usuário para usuário.

>[!IMPORTANT]
>
> Esses endereços IP podem mudar no futuro e podem não ser os mesmos para usuários em diferentes regiões geográficas.


## ETAPA 2.  Simulação do ambiente de pré-qualificação para produção {#spoofing-the-prequalification-environment}

* Edite o *c:\\windows\\System32\\drivers\\etc\\hosts* (no Windows) ou */etc/hosts* (em Macintosh/Linux/Android) e adicione o seguinte:

* Simular perfil de produção
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Falsificação no Android:** Para falsificar no Android, você precisa usar um emulador de Android.

* Quando a falsificação estiver em vigor, você poderá simplesmente usar os URLs comuns para os perfis de produção e preparo: (ou seja, `http://sp.auth-staging.adobe.com` e `http://entitlement.auth-staging.adobe.com` e você chegará ao botão *ambiente/produção de pré-qualificação* da* nova build.


## ETAPA 3.  Verifique se você está apontando para o ambiente correto {#Verify-you-are-pointing-to-the-right-environment}

**Esta é uma etapa fácil:**

* carregar [ambiente pré-igual de direitos](https://entitlement-prequal.auth.adobe.com/environment.html) e [direito](https://entitlement.auth.adobe.com/environment.html). Eles devem retornar a mesma resposta.


## ETAPA 4.  Executar um fluxo de autenticação/autorização simples usando o site do programador {#peform-a-simple-auth-flow}

* Esta etapa requer o endereço do site do programador e algumas credenciais MVPD válidas (um usuário que seja autenticado e autorizado).

## ETAPA 5.  Realizar testes de cenário usando os sites do programador {#perform-scenario-testing-using-programmer-website}

* Depois de concluir a configuração do ambiente e garantir que o fluxo básico de autenticação-autorização esteja funcionando, você pode prosseguir com os testes de cenários mais complexos.


## ETAPA 6.  Realizar testes usando o site de teste da API {#perform-testing-using-api-testing-site}

* Se quiser aprofundar no teste da autenticação do Adobe Primetime, recomendamos que você use o [Site de teste da API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Você pode encontrar mais detalhes no site de teste da API em [Como testar fluxos de autenticação e autorização usando o site de teste da API do Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).
