---
description: O recurso de Inserção de ad break parcial (PABI, Parcial Ad Break Insertion) imita uma experiência semelhante a uma TV, na qual, se o usuário ingressar em um stream ao vivo dentro de um intervalo intermediário, o usuário é exibido para anúncios intermediários em vez de um anúncio precedente ou tabuleiro.
title: Inserção parcial de quebra de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Inserção parcial de quebra de anúncio {#partial-ad-break-insertion}

O recurso de Inserção de ad break parcial (PABI, Parcial Ad Break Insertion) imita uma experiência semelhante a uma TV, na qual, se o usuário ingressar em um stream ao vivo dentro de um intervalo intermediário, o usuário é exibido para anúncios intermediários em vez de um anúncio precedente ou tabuleiro.

Quando o servidor de publicidade retorna anúncios precedentes para um fluxo ao vivo, o servidor de manifesto injetará o ad break precedente antes do ponto ao vivo e inserirá a tag EXT-X-START com seu valor TIMEOFFSET apontando para o início do ad break precedente. Esse comportamento padrão garante que todo o ad break precedente seja reproduzido antes do conteúdo no ponto ativo. Se um usuário ingressar em um fluxo quando o ponto ativo estiver próximo a um ad break intermediário, será mostrado ao usuário o ad break precedente antes do ad break intermediário no ponto ativo.

O recurso PABI instrui o servidor manifest a ignorar o ad break precedente e definir o valor EXT-X-START:TIMEOFFSET para o início do anúncio intermediário presente no ponto ativo. Isso garante que o usuário visualize todo o anúncio intermediário que está sendo reproduzido no ponto de acesso sem precisar visualizar o ad break precedente.

>[!NOTE]
>
>Essa funcionalidade só está disponível para fluxos ao vivo. O servidor manifest insere o ad break precedente na lista de reprodução de VOD por padrão.

>[!NOTE]
>
>Para ativar o PABI, será necessário especificar o [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) no URL de inicialização.

>[!NOTE]
>
>O [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) é uma tag HLS padrão que indica um ponto de partida preferencial na lista de reprodução.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Use o rastreamento no lado do cliente porque ele tem mais controle sobre o acionamento dos beacons de rastreamento.
* As quebras parciais de anúncios só devem ser usadas com o modo de rastreamento do lado do servidor se o reprodutor suportar EXT-X-START.