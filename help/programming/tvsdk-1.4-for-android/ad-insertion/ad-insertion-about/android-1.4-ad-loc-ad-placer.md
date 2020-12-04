---
description: Há algumas maneiras de determinar a inserção e a colocação do anúncio.
seo-description: Há algumas maneiras de determinar a inserção e a colocação do anúncio.
seo-title: Inserção e posicionamento do anúncio
title: Inserção e posicionamento do anúncio
uuid: 1d4d6364-1c49-402b-9b72-8c185b1c94e1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Inserção e posicionamento do anúncio{#ad-insertion-and-placement}

Há algumas maneiras de determinar a inserção e a colocação do anúncio.

## Inserção de anúncio {#section_1F7581B987704E318E064082190E8243}

Esta é uma visão geral do processo usado para determinar a inserção de anúncios:

1. **Detecção** de oportunidade: O TVSDK usa informações de fluxo para detectar locais possíveis e desejados para anúncios.
1. **Resolução** do anúncio: O TVSDK se comunica com um servidor de publicidade para recuperar os anúncios a serem divididos no conteúdo.
1. **Posicionamento** do anúncio: O TVSDK carrega os anúncios especificados e os coloca em pausas de anúncio na linha do tempo do conteúdo nos locais especificados e recompata a linha do tempo virtual, se necessário.

## Posicionamento do anúncio {#section_B9D63F7409A2447F9FF209289BE5D3D5}

O TVSDK pode obter locais para possíveis posicionamentos de anúncios das seguintes fontes:

* **Metadados/dicas do manifesto**

   O TVSDK detecta as dicas, extrai as informações necessárias dessas dicas e se comunica com um servidor de publicidade para obter os anúncios correspondentes. Essa fonte é comum para fluxos ao vivo/lineares.

   O TVSDK geralmente substitui o conteúdo principal pelos anúncios no local indicado pelos metadados/dicas; caso contrário, o cliente cairia cada vez mais atrás do ponto real.

* **O mapa do servidor de publicidade**

   Normalmente, os metadados sobre esses fluxos são registrados no servidor de publicidade antes da reprodução. O TVSDK recupera a linha do tempo do anúncio e os anúncios correspondentes do servidor. Essa fonte é comum para fluxos VOD.

   O TVSDK normalmente insere os anúncios resolvidos no conteúdo principal, conforme indicado pelo mapa do servidor.

>[!NOTE]
>
>Por padrão, o TVSDK usa dicas manifestas para fluxos ao vivo/lineares e mapas de servidor de publicidade para fluxos VOD. Entretanto, para oferecer suporte à reprodução de evento completo para eventos ao vivo, seu aplicativo deve executar etapas extras.

