---
description: Há algumas maneiras de determinar a inserção e o posicionamento do anúncio.
title: Inserção e posicionamento do anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Inserção e posicionamento de anúncios{#ad-insertion-and-placement}

Há algumas maneiras de determinar a inserção e o posicionamento do anúncio.

## Inserção de anúncio {#section_1F7581B987704E318E064082190E8243}

Esta é uma visão geral do processo usado para determinar a inserção de anúncios:

1. **Detecção** de oportunidades: O TVSDK usa informações de fluxo para detectar locais possíveis e desejados para anúncios.
1. **Resolução** do anúncio: O TVSDK se comunica com um servidor de anúncios para recuperar os anúncios para dividir no conteúdo.
1. **Inserção** do anúncio: O TVSDK carrega os anúncios especificados e os coloca em quebras de anúncios na linha do tempo do conteúdo nos locais especificados e recalcula a linha do tempo virtual, se necessário.

## Inserção de anúncio {#section_B9D63F7409A2447F9FF209289BE5D3D5}

O TVSDK pode obter locais para possíveis posicionamentos de anúncios das seguintes fontes:

* **Metadados/dicas do manifesto**

   O TVSDK detecta as dicas, extrai as informações necessárias dessas dicas e se comunica com um servidor de publicidade para obter os anúncios correspondentes. Essa fonte é comum para fluxos ao vivo/lineares.

   O TVSDK geralmente substitui o conteúdo principal pelos anúncios no local indicado pelos metadados/dicas; caso contrário, o cliente deixaria cada vez mais atrás do ponto de entrada real.

* **O mapa do servidor de publicidade**

   Normalmente, os metadados sobre esses fluxos são registrados no servidor de publicidade antes da reprodução. O TVSDK recupera a linha do tempo do anúncio e os anúncios correspondentes do servidor. Essa fonte é comum para fluxos VOD.

   O TVSDK normalmente insere os anúncios resolvidos no conteúdo principal, conforme indicado pelo mapa do servidor.

>[!NOTE]
>
>Por padrão, o TVSDK usa dicas de manifesto para fluxos ao vivo/lineares e mapas do servidor de publicidade para fluxos VOD. No entanto, para oferecer suporte à repetição completa de eventos para eventos ao vivo, o aplicativo deve realizar etapas adicionais.

