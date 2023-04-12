---
title: Notas de versão da autenticação da Adobe Primetime 2.63
description: Notas de versão da autenticação da Adobe Primetime 2.63
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Notas de versão da Autenticação Adobe Primetime 2.63 {#pt-authn-263-rn}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

Esta página descreve novos recursos, alterações e problemas conhecidos com esta versão:

## Lado do servidor e clientes da Web {#server-side-web-clients-263}

* [Número da build](#build-number)
* [Novos recursos](#new-features)

### Número da build {#build-number-263}

Autenticação Adobe Primetime: adobe-pass-**2,63**
Data de lançamento: **20/09/2022 - 09/22/2022**

### Novos recursos {#new-features-263}

#### Melhore o mecanismo de identificação da plataforma {#pf-identification-mech}

* A partir desta versão, aprimoramos o mecanismo usado para identificar um dispositivo e não dependerá mais da implementação do lado do cliente. Isso fornecerá uma granularidade mais precisa ao aplicar regras de negócios no nível da plataforma e uma melhor compreensão dos valores de tráfego nos relatórios ESM.

* Uma nova versão do ESM será lançada em breve, com relatórios novos e aprimorados que expõem os campos relacionados à plataforma.

* Para obter mais detalhes sobre as alterações planejadas, entre em contato com o TAM.

#### Autodegradação MVPD {#mvpd-self-degradation}

Esse recurso fornece aos MVPDs a capacidade de ignorar temporariamente seus próprios pontos de extremidade de autenticação e autorização para cenários de tráfego alto quando a carga nesses pontos finais se tornar muito alta.


#### Adicionar ID de proxy no cabeçalho das chamadas de autorização {#add-proxied-id}

Esse recurso adiciona a id de um MVPD associado do Synacor no cabeçalho da chamada de autorização. Isso permite que o Synacor configure regras de negócios para cada proxy individual (por exemplo, roteamento para domínios diferentes por MVPD proxy).


#### Painel TVE {#tve-dashboard}

Nesta versão, corrigimos um problema em que authN ou authZ TTL definido no nível MVPD não eram computados corretamente nos relatórios de configuração.


#### JavaScript SDK 4.6.0 {#js-sdk}

* Remoção do uso de `eval` , tornando o SDK compatível com a Política de segurança de conteúdo.
* Correção de um problema que impedia que o fluxo de Autenticação terminasse com sucesso quando o Armazenamento local do navegador era explicitamente limpo por um aplicativo de parceiro.



