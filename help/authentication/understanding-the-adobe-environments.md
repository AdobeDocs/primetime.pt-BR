---
title: Compreensão dos ambientes do Adobe
description: Compreensão dos ambientes do Adobe
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Compreensão dos ambientes do Adobe {#understanding-the-adobe-environments}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

A documentação oficial que descreve os ambientes do Adobe está disponível [Configuração do ambiente e teste em pré-igual](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md):

Os ambientes Adobe, resumidos em poucas palavras:

O Adobe tem dois ambientes: **Pré-qualificação** e **Versão**.

* No ambiente de Pré-qualificação, estamos preparando a nova build para ser lançada.

* A build da versão atual está no ambiente Versão.

Cada ambiente tem dois perfis : **preparo** e **produção**.

* O perfil de preparo se conecta ao servidor de preparo MVPDs
* O perfil de produção se conecta ao perfil de produção de MVPDs.

A razão para ter os dois perfis é que no perfil de preparo estamos preparando novos parceiros para entrar em funcionamento, e eles gostariam de testar o sistema com a próxima build (Pré-qualificação) ou com a versão um (mais estável).

Se um parceiro quiser testar a nova versão, há algumas etapas adicionais que precisam ser feitas. Consulte [Configuração do ambiente e teste em pré-igual](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

Ao seguir as etapas acima, é garantido que a próxima versão será testada no ambiente de Pré-qualificação.
