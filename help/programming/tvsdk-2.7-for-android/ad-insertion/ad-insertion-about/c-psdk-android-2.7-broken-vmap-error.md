---
description: Quando o TVSDK encontra um VMAP quebrado em uma resposta de servidor de publicidade, ele despacha um erro 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;QUEBROU O VMAP
title: Tratamento de erros do cliente para VMAP com falha
exl-id: 268307a9-b72e-45fa-84f2-a8e7d969e2ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Tratamento de erros do cliente para VMAP com falha {#client-error-handling-for-broken-vmap}

Quando o TVSDK encontra um VMAP quebrado em uma resposta de servidor de publicidade, ele despacha um erro 1109 (NETWORK_AD_URL_FAILED).

Dependendo da natureza da resposta do servidor de anúncios e das configurações de carregamento de anúncios, o reprodutor pode receber números diferentes de erros 1109 quando o TVSDK encontra um VMAP com falha em uma resposta do servidor de anúncios.

Vamos considerar um cenário em que a resposta do servidor de publicidade aponte para o XML do VMAP. Digamos também que a resposta do servidor de anúncios tenha quatro slots de anúncios disponíveis, cada um apontando para o mesmo VMAP. Finalmente, digamos que esse VMAP esteja corrompido.

Nesse cenário, se a resolução de anúncios lentos estiver ativada ( [Habilitar resolução de anúncios lentos](../../../tvsdk-2.7-for-android/ad-insertion/c-psdk-android-2.7-lazy-ad-resolving/t-psdk-android-2.7-enable-lazy-ad-resolving.md)), o TVSDK despachará dois erros 1109 (não um como esperado): um erro é despachado em cada passagem de análise pela linha do tempo. Isso ocorre porque quando a resolução de anúncios lentos está habilitada, o TVSDK analisa os anúncios em duas passagens: a primeira passagem ocorre antes do início da reprodução do conteúdo para anúncios precedentes e a segunda passagem ocorre após o início da reprodução, para anúncios intermediários e posteriores.

>[!NOTE]
>
>Nesse cenário, se você desativar a resolução de anúncios lentos, o TVSDK acionará apenas um erro 1109 (apenas um passo de análise).
