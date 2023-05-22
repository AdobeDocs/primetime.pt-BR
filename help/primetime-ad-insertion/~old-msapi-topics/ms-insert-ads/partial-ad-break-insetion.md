---
description: O recurso de Inserção parcial de ad break (PABI) imita uma experiência semelhante a uma TV na qual, se o usuário ingressar em um stream ao vivo dentro de uma interrupção durante a exibição, o usuário verá anúncios durante a exibição em vez de um anúncio ou tabulação antes da exibição.
title: Inserção de ad break parcial
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Inserção de ad break parcial {#partial-ad-break-insertion}

O recurso de Inserção parcial de ad break (PABI) imita uma experiência semelhante a uma TV na qual, se o usuário ingressar em um stream ao vivo dentro de uma interrupção durante a exibição, o usuário verá anúncios durante a exibição em vez de um anúncio ou tabulação antes da exibição.

Quando o servidor de anúncios retorna anúncios precedentes para um fluxo ao vivo, o servidor de manifesto injetará o ad break precedente antes do ponto ao vivo e inserirá a tag EXT-X-START com seu valor TIMEOFFSET apontando para o início do ad break precedente. Esse comportamento padrão garante que todo o ad break precedente seja reproduzido antes do conteúdo no ponto de acesso. Se um usuário ingressar em um fluxo quando o ponto de acesso estiver próximo a um ad break intermediário, o usuário verá o ad break precedente antes do ad break intermediário no ponto de acesso.

O recurso PABI instrui o servidor de manifesto a ignorar o ad break precedente e definir o valor EXT-X-START:TIMEOFFSET para o início do anúncio intermediário presente no ponto ativo. Isso garante que o usuário veja todo o anúncio intermediário sendo reproduzido no momento no ponto de acesso, sem precisar exibir o ad break precedente.

>[!NOTE]
>
>Essa funcionalidade só está disponível para transmissões em tempo real. Por padrão, o servidor de manifesto insere o ad break precedente no topo da lista de reprodução de VOD.

>[!NOTE]
>
>Para habilitar o PABI, será necessário especificar o [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) no URL de inicialização.

>[!NOTE]
>
>A variável [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) é uma tag HLS padrão que indica um ponto de partida preferencial na lista de reprodução.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Usar o rastreamento do lado do cliente porque o cliente tem mais controle sobre o acionamento de beacons de rastreamento.
* Os ad breaks parciais só devem ser usados com o modo de rastreamento do lado do servidor se o reprodutor suportar EXT-X-START.