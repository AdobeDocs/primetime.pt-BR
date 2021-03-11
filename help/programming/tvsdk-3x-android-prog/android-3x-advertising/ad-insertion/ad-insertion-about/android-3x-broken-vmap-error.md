---
description: Quando o TVSDK encontra um VMAP quebrado em uma resposta de servidor de publicidade, ele despacha um erro 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;VMAP quebrado
title: Tratamento de erros do cliente para VMAP quebrado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Tratamento de erros do cliente para VMAP quebrado {#client-error-handling-for-broken-vmap}

Quando o TVSDK encontra um VMAP quebrado em uma resposta de servidor de publicidade, ele despacha um erro 1109 (NETWORK_AD_URL_FAILED).

Dependendo da natureza da resposta do servidor de anúncios e de suas configurações de carregamento de anúncios, o reprodutor poderá receber números diferentes de erros 1109 quando o TVSDK encontrar um VMAP quebrado em uma resposta do servidor de anúncios.

Considere um cenário em que a resposta do servidor de anúncios aponta para VMAP XML. Digamos também que a resposta do servidor de anúncios tenha quatro slots de anúncio disponíveis, cada um deles apontando para o mesmo VMAP. Finalmente, digamos que esse VMAP está quebrado.

Nesse cenário, se a resolução de anúncios ociosos estiver ativada ([Ativar anúncio preguiçoso resolvendo](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)), o TVSDK despachará dois erros 1109 (não um como seria de esperar): um erro é despachado em cada análise que passa pela linha do tempo. Isso ocorre porque quando a resolução de anúncio lento é ativada, o TVSDK analisa os anúncios em 2 passagens: a primeira passagem acontece pouco antes do início da reprodução do conteúdo para anúncios precedentes e a segunda passagem acontece após o início da reprodução, para anúncios intermediários e posteriores à exibição.

>[!NOTE]
>
>Nesse cenário, se você desativar a resolução de anúncios preguiçosos, o TVSDK acionará apenas um erro 1109 (apenas uma passagem de análise).