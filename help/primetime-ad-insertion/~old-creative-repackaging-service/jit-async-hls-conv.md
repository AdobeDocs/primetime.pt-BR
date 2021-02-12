---
description: O CRS fornece JIT (just-in-time) e reempacotamento assíncrono e conversão de HLS para HLS. O resultado do reempacotamento é uma versão formatada HLS do anúncio original. O CRS coloca a versão formatada do HLS no servidor de rede do delivery de conteúdo (CDN) para uso quando necessário.
seo-description: O CRS fornece JIT (just-in-time) e reempacotamento assíncrono e conversão de HLS para HLS. O resultado do reempacotamento é uma versão formatada HLS do anúncio original. O CRS coloca a versão formatada do HLS no servidor de rede do delivery de conteúdo (CDN) para uso quando necessário.
seo-title: Principais utilizações do SIR
title: Principais utilizações do SIR
uuid: df2caa67-bc94-4146-9b93-14edc060c3d5
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Principais usos do CRS {#main-uses-of-crs}

O CRS fornece JIT (just-in-time) e reempacotamento assíncrono e conversão de HLS para HLS. O resultado do reempacotamento é uma versão formatada HLS do anúncio original. O CRS coloca a versão formatada do HLS no servidor de rede do delivery de conteúdo (CDN) para uso quando necessário.

Em JIT, reempacotar o Adobe Primetime e inserir o anúncio inicia o processo de reempacotamento quando ele encontra pela primeira vez um anúncio não HLS. Isso geralmente implica oportunidades perdidas de executar o anúncio durante o processo de reempacotamento.

Na reembalagem assíncrona, o anúncio é transcodificado e armazenado antes de ser necessário, o que pode eliminar as oportunidades perdidas.

Na conversão HLS para HLS, o CRS reformata um anúncio HLS e é criativo em partes de tamanho apropriado para garantir uma reprodução consistente.

## Reempacotamento just-in-time {#section_1BA344F2300B49F291865A7461EDFEAE}

A sequência para reempacotamento JIT é a seguinte:

1. O servidor manifest busca um anúncio.
1. Se o formato do anúncio for HLS, o servidor manifest inserirá o anúncio no fluxo de conteúdo.
1. Se o formato não for HLS (por exemplo, MP4, FLV ou WebM), o servidor manifest procurará uma versão transcodificada no servidor CDN. Se encontrar um, ele insere o anúncio transcodificado no fluxo de conteúdo.
1. Se o formato não for HLS e o servidor CDN não tiver uma versão transcodificada, o servidor manifest transmitirá o anúncio para CRS, o que transcodificará o anúncio criativo e armazenará o resultado no servidor CDN para uso posterior.
1. O servidor manifest retorna o conteúdo sem o anúncio.

## Reempacotamento assíncrono {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Você pode usar a API descrita em [Reempacotar API](../~old-creative-repackaging-service/api-repackage.md) para pré-transcodificar um anúncio não HLS para minimizar a perda de impressões e maximizar a monetização.

## Conversão HLS para HLS {#section_877A0E7E8FAF4C2DB086A31C24D53435}

Para evitar buffering e atraso, um cliente baixa um vídeo em pequenos pedaços. Se os tamanhos de segmentos forem inconsistentes, a reprodução pode estar irregular. A conversão HLS para HLS garante que os blocos de dados tenham a mesma duração (por exemplo, 6 segundos).

>[!NOTE]
>
>O CRS produz HLS versão 3, independentemente da versão HLS que recebe.