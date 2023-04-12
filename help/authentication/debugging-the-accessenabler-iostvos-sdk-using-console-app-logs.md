---
title: Depuração do SDK do AccessEnabler iOS/tvOS usando registros de aplicativos do Console
description: Depuração do SDK do AccessEnabler iOS/tvOS usando registros de aplicativos do Console
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# Depuração do SDK do AccessEnabler iOS/tvOS usando registros de aplicativos do Console {#debugging-the-accessenabler-iostvos-sdk-using-console-app-logs}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.


## Visão geral

O escopo deste documento é capturar e apresentar a evolução do mecanismo de registro do SDK do iOS/tvOS do AccessEnabler junto com alguns detalhes úteis para depurar a estrutura do AccessEnabler usando os logs de aplicativo do Console.

## Estado do mecanismo de registro

A finalidade do mecanismo de registro do AccessEnabler iOS/tvOS é emitir mensagens úteis para solucionar possíveis problemas que um aplicativo que usa a estrutura AccessEnabler poderia encontrar devido a ele.

### AccessEnabler iOS/tvOS 3.5.0 e superior

A partir da versão 3.5.0 do AccessEnabler iOS/tvOS, o mecanismo de registro apresenta as seguintes melhorias à medida que as alterações são feitas:

* A estrutura AccessEnabler usa Apple recomendado [OSLog](https://developer.apple.com/documentation/os/oslog) implementação.

* A estrutura AccessEnabler apresenta a capacidade de filtrar logs de aplicativos do Console com base no Subsistema: **com.adobe.pass.AccessEnabler**. Todas as mensagens emitidas pelo SDK fazem parte do com.adobe.pass.AccessEnabler.

* A estrutura AccessEnabler apresenta a capacidade de filtrar logs de aplicativos do Console com base em Qualquer (prefixo): **[AccessEnabler]**. Todas as mensagens emitidas pelo SDK recebem o prefixo [AccessEnabler].

* A estrutura AccessEnabler apresenta a capacidade de filtrar logs de aplicativos do Console com base em Categoria: **depurar**, **erro** em conjugação com qualquer um dos dois critérios acima referidos: Subsistema ou Qualquer (prefixo).

## Depuração usando registros de aplicativo do Console

Dependendo dos problemas que são investigados, você pode querer incluir ou excluir as mensagens de registro emitidas pela estrutura AccessEnabler , portanto, você pode encontrar abaixo alguns detalhes úteis que podem ajudá-lo durante as investigações e ao usar logs de aplicativos do Console.


### AccessEnabler iOS/tvOS 3.5.0 e superior

#### Incluindo {#including}

Primeiro de tudo para poder ver qualquer mensagem de registro emitida pela estrutura do AccessEnabler para você **must** selecione &quot;Include Info Messages&quot; e &quot;Include Debug Messages&quot; na seção Action do aplicativo Console, conforme apresentado na imagem abaixo.

![](assets/include-info-debug-msg.png)


Para poder depurar a funcionalidade do SDK do AccessEnabler iOS/tvOS e **see** a estrutura do AccessEnabler permite:

* Pesquisar no aplicativo do Console usando **Subsistema** que equivale ao valor com.adobe.pass.AccessEnabler como na imagem abaixo.

![](assets/subsys-console-app.png)

* Pesquisar no aplicativo do Console usando **Qualquer** que contém a opção
   [AccessEnabler] como na imagem abaixo.

![](assets/any-optn-console-app.png)

Além dos dois critérios acima, você também pode usar o **Categoria** em conjugação com **Subsistema** ou **Qualquer (prefixo)** para pesquisar explicitamente **depurar** ou **erro** mensagens de nível emitidas pelo SDK do AccessEnabler iOS/tvOS.

#### Excluir

Para poder depurar melhor a funcionalidade de outros componentes e **exclude** a estrutura do AccessEnabler permite:

* Pesquisar no aplicativo do Console usando **Subsistema** opção que não é igual ao valor com.adobe.pass.AccessEnabler .
* Pesquisar no aplicativo do Console usando **Qualquer** que não contém a opção [AccessEnabler] valor.

## Relatório de um problema

Ao relatar um problema à Autenticação do Adobe Primetime, considere as seguintes sugestões:

* tente fornecer as etapas de reprodução.
* tente fornecer as versões do sistema operacional e os modelos de dispositivo nos quais o problema ocorre.
* tente fornecer a versão do SDK do AccessEnabler iOS/tvOS que apresenta o problema.
* tente capturar e anexar todas as mensagens de registro do SDK do AccessEnabler iOS/tvOS usando qualquer uma das duas opções apresentadas no [Incluindo](#including) seção.
