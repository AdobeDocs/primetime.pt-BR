---
description: Há algumas maneiras de determinar a inserção e o posicionamento do anúncio.
title: Inserção e posicionamento de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Inserção e posicionamento de anúncios{#ad-insertion-and-placement}

Há algumas maneiras de determinar a inserção e o posicionamento do anúncio.

## Inserção de anúncio {#section_1F7581B987704E318E064082190E8243}

Esta é uma visão geral do processo usado para determinar a inserção de anúncios:

1. **Detecção de oportunidade**: o TVSDK usa informações de fluxo para detectar locais possíveis e desejados para anúncios.
1. **Resolução do anúncio**: O TVSDK se comunica com um servidor de anúncios para recuperar os anúncios e dividi-los no conteúdo.
1. **Posicionamento do anúncio**: O TVSDK carrega os anúncios especificados e os coloca em ad breaks na linha do tempo do conteúdo nos locais especificados e recalcula a linha do tempo virtual, se necessário.

## Posicionamento do anúncio {#section_B9D63F7409A2447F9FF209289BE5D3D5}

O TVSDK pode obter locais para possível posicionamento de anúncios das seguintes fontes:

* **Manifestar metadados/dicas**

  O TVSDK detecta as dicas, extrai as informações necessárias dessas dicas e se comunica com um servidor de publicidade para obter os anúncios correspondentes. Essa fonte é comum para fluxos ao vivo/lineares.

  O TVSDK geralmente substitui o conteúdo principal pelos anúncios no local indicado pelos metadados/dicas; caso contrário, o cliente ficaria cada vez mais atrás do ponto ativo real.

* **O mapa do servidor de publicidade**

  Normalmente, os metadados sobre esses fluxos são registrados no servidor de publicidade antes da reprodução. O TVSDK recupera a linha do tempo do anúncio e os anúncios correspondentes do servidor. Essa fonte é comum para fluxos de VOD.

  O TVSDK geralmente insere os anúncios resolvidos no conteúdo principal, conforme indicado pelo mapa do servidor.

>[!NOTE]
>
>Por padrão, o TVSDK usa dicas de manifesto para fluxos ao vivo/lineares e mapas de servidor de publicidade para fluxos de VOD. No entanto, para oferecer suporte à reprodução de evento completo para eventos ao vivo, seu aplicativo deve seguir etapas adicionais.
