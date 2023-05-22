---
description: O CRS fornece reempacotamento just-in-time (JIT) e assíncrono e conversão de HLS para HLS. O resultado do reempacotamento é uma versão HLS formatada do criativo do anúncio original. O CRS coloca a versão formatada HLS no servidor da rede de entrega de conteúdo (CDN) para uso quando necessário.
title: Principais utilizações dos SIR
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Principais utilizações dos SIR {#main-uses-of-crs}

O CRS fornece reempacotamento just-in-time (JIT) e assíncrono e conversão de HLS para HLS. O resultado do reempacotamento é uma versão HLS formatada do criativo do anúncio original. O CRS coloca a versão formatada HLS no servidor da rede de entrega de conteúdo (CDN) para uso quando necessário.

No reempacotamento JIT, a inserção de anúncios do Adobe Primetime inicia o processo de reempacotamento quando encontra pela primeira vez um criativo de anúncios não HLS. Isso geralmente acarreta perda de oportunidades para executar o anúncio durante o processo de reempacotamento.

No reempacotamento assíncrono, o anúncio criativo é transcodificado e armazenado antes que seja necessário, o que pode eliminar essas oportunidades perdidas.

Na conversão de HLS para HLS, o CRS reformata um anúncio de HLS em blocos de tamanho apropriado para garantir uma reprodução consistente.

## Reempacotamento Just-in-Time {#section_1BA344F2300B49F291865A7461EDFEAE}

A sequência para o reempacotamento de JIT é a seguinte:

1. O servidor de manifesto busca um anúncio.
1. Se o formato do anúncio for HLS, o servidor de manifesto insere o anúncio no fluxo de conteúdo.
1. Se o formato não for HLS (por exemplo, MP4, FLV ou WebM), o servidor de manifesto procurará uma versão transcodificada no servidor CDN. Se encontrar um, ele insere o anúncio transcodificado no fluxo de conteúdo.
1. Se o formato não for HLS e o servidor CDN não tiver uma versão transcodificada, o servidor de manifesto transmitirá o anúncio para o CRS, que transcodifica a criação do anúncio e armazena o resultado no servidor CDN para uso posterior.
1. O servidor de manifesto retorna o conteúdo sem o anúncio.

## Reempacotamento assíncrono {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Você pode usar a API descrita em [API de reempacotamento](../~old-creative-repackaging-service/api-repackage.md) pré-transcodificar uma ferramenta criativa não HLS para minimizar a perda de impressões e maximizar a monetização.

## Conversão de HLS para HLS {#section_877A0E7E8FAF4C2DB086A31C24D53435}

Para evitar buffering e atraso, um cliente baixa um vídeo em pequenos pedaços. Se os tamanhos dos blocos forem inconsistentes, a reprodução poderá ser irregular. A conversão de HLS em HLS garante que os fragmentos de dados tenham a mesma duração (por exemplo, 6 segundos).

>[!NOTE]
>
>O CRS produz HLS versão 3, independentemente de qual versão do HLS ele recebe.