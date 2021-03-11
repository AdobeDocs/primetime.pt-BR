---
description: O CRS fornece JIT (just-in-time), reempacotamento assíncrono e conversão de HLS para HLS. O resultado de um reempacotamento é uma versão formatada em HLS do anúncio original. O CRS coloca a versão formatada do HLS no servidor da rede de entrega de conteúdo (CDN) para uso quando necessário.
title: Principais utilizações do SIR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Principais utilizações do SIR {#main-uses-of-crs}

O CRS fornece JIT (just-in-time), reempacotamento assíncrono e conversão de HLS para HLS. O resultado de um reempacotamento é uma versão formatada em HLS do anúncio original. O CRS coloca a versão formatada do HLS no servidor da rede de entrega de conteúdo (CDN) para uso quando necessário.

Em JIT, o reempacotamento de anúncios do Adobe Primetime começa o processo de reempacotamento quando ele encontra pela primeira vez um anúncio não HLS. Isso geralmente implica a perda de oportunidades para executar o anúncio durante o processo de reempacotamento.

Em reembalagens assíncronas, o anúncio é transcodificado e armazenado antes de ser necessário, o que pode eliminar as oportunidades perdidas.

Na conversão de HLS em HLS, o CRS reformata um anúncio de HLS e o cria em partes do tamanho apropriado para garantir uma reprodução consistente.

## Reempacotamento just-in-time {#section_1BA344F2300B49F291865A7461EDFEAE}

A sequência para reempacotamento JIT é a seguinte:

1. O servidor manifest busca um anúncio.
1. Se o formato do anúncio for HLS, o servidor de manifesto insere o anúncio no fluxo de conteúdo.
1. Se o formato não for HLS (por exemplo, MP4, FLV ou WebM), o servidor de manifesto procurará uma versão transcodificada no servidor CDN. Se encontrar um, ele insere o anúncio transcodificado no fluxo de conteúdo.
1. Se o formato não for HLS e o servidor CDN não tiver uma versão transcodificada, o servidor de manifesto transmitirá o anúncio para CRS, o que transcodificará o anúncio criativo e armazenará o resultado no servidor CDN para uso posterior.
1. O servidor de manifesto retorna o conteúdo sem o anúncio.

## Reempacotamento assíncrono {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Você pode usar a API descrita em [Repackaging API](../~old-creative-repackaging-service/api-repackage.md) para pré-transcodificar um anúncio não-HLS para minimizar a perda de impressões e maximizar a monetização.

## Conversão de HLS para HLS {#section_877A0E7E8FAF4C2DB086A31C24D53435}

Para evitar buffering e atraso, um cliente baixa um vídeo em pequenas partes. Se os tamanhos do bloco forem inconsistentes, a reprodução pode ser turva. A conversão de HLS em HLS garante que os blocos de dados tenham a mesma duração (por exemplo, 6 segundos).

>[!NOTE]
>
>O CRS produz HLS versão 3, independentemente da versão do HLS que recebe.