---
description: O recurso Inserção parcial de quebra de anúncio (PABI) imita uma experiência semelhante à TV na qual, se o usuário ingressar em um fluxo ao vivo dentro de uma pausa intermediária, o usuário será exibido para anúncios intermediários em vez de um anúncio precedente ou uma ardósia.
seo-description: O recurso Inserção parcial de quebra de anúncio (PABI) imita uma experiência semelhante à TV na qual, se o usuário ingressar em um fluxo ao vivo dentro de uma pausa intermediária, o usuário será exibido para anúncios intermediários em vez de um anúncio precedente ou uma ardósia.
seo-title: Inserção parcial de quebra de anúncio
title: Inserção parcial de quebra de anúncio
uuid: a0c1ae34-0f8d-4401-97fe-45a2ea40d08d
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Inserção parcial de quebra de anúncio {#partial-ad-break-insertion}

O recurso Inserção parcial de quebra de anúncio (PABI) imita uma experiência semelhante à TV na qual, se o usuário ingressar em um fluxo ao vivo dentro de uma pausa intermediária, o usuário será exibido para anúncios intermediários em vez de um anúncio precedente ou uma ardósia.

Quando o servidor de publicidade retorna anúncios precedentes para um fluxo ao vivo, o servidor de manifesto injetará o intervalo do anúncio precedente antes do ponto ao vivo e inserirá a tag EXT-X-START com seu valor TIMEOFFSET apontando para o start do intervalo do anúncio precedente. Esse comportamento padrão garante que todo o intervalo do anúncio precedente seja reproduzido antes do conteúdo no ponto ativo. Se um usuário ingressar em um fluxo quando o ponto ativo estiver próximo a um intervalo de anúncios intermediário, o usuário receberá a pausa do anúncio precedente antes da pausa do anúncio intermediário no ponto ativo.

O recurso PABI instrui o servidor manifest a ignorar a quebra de anúncio precedente e a definir o valor EXT-X-START:TIMEOFFSET para o início da propaganda intermediária presente no ponto ativo. Isso garante que o usuário visualize todo o anúncio intermediário que está sendo reproduzido no ponto ativo sem ter que visualização no intervalo do anúncio precedente.

>[!NOTE]
>
>Essa funcionalidade só está disponível para fluxos ao vivo. Por padrão, o servidor manifest insere a quebra de anúncio precedente na lista de reprodução VOD.

>[!NOTE]
>
>Para ativar o PABI, será necessário especificar [query_params](../../msapi-topics/ms-getting-started/ms-api-query-params.md) no URL de inicialização.

>[!NOTE]
>
>O [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) é uma tag HLS padrão que indica um ponto de partida preferencial na lista de reprodução.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Use o rastreamento do cliente porque o cliente tem mais controle sobre o acionamento dos beacons de rastreamento.
* Quebras parciais de anúncios só devem ser usadas com o modo de rastreamento do lado do servidor se o player suportar EXT-X-START.