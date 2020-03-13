---
description: Quando o TVSDK encontra um VMAP quebrado em uma resposta de servidor de publicidade, ele despacha um erro 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: Quando o TVSDK encontra um VMAP quebrado em uma resposta de servidor de publicidade, ele despacha um erro 1109 (NETWORK_AD_URL_FAILED).
seo-title: Tratamento de erros do cliente para VMAP quebrado
title: Tratamento de erros do cliente para VMAP quebrado
uuid: ab2c567d-d945-4ebe-b65a-c1f13518a576
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Tratamento de erros do cliente para VMAP quebrado {#client-error-handling-for-broken-vmap}

Quando o TVSDK encontra um VMAP quebrado em uma resposta de servidor de publicidade, ele despacha um erro 1109 (NETWORK_AD_URL_FAILED).

Dependendo da natureza da resposta do servidor de publicidade e das configurações de carregamento de seu anúncio, o player poderá receber números diferentes de 1109 erros quando o TVSDK encontrar um VMAP quebrado em uma resposta do servidor de publicidade.

Vamos considerar um cenário em que a resposta do servidor de anúncios aponte para VMAP XML. Digamos também que a resposta do servidor de anúncios tenha quatro slots de anúncio disponíveis, cada um deles apontando para o mesmo VMAP. Finalmente, digamos que esse VMAP está quebrado.

Nesse cenário, se a resolução de anúncios ociosos estiver ativada ([Ativar resolução](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)de anúncios ociosos), o TVSDK enviará dois erros 1109 (não um como seria esperado): um erro é despachado em cada passagem de análise na linha do tempo. Isso ocorre porque quando a resolução de anúncios ociosos está ativada, o TVSDK analisa os anúncios em 2 passagens: a primeira passagem acontece pouco antes do início da reprodução do conteúdo para anúncios precedentes e a segunda passagem acontece após o início da reprodução, para anúncios intermediários e posteriores.

>[!NOTE]
>
>Nesse cenário, se você desativar a resolução de anúncios preguiçosos, o TVSDK acionará apenas um erro 1109 (apenas uma passagem de análise).