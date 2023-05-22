---
description: Embora o cenário padrão do serviço de reempacotamento criativo (CRS) seja usar uma Rede de entrega de conteúdo (CDN), você pode implantar ativos de CRS em mais de uma CDN.
title: Suporte a várias CDNs para entrega de anúncios CRS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Suporte a várias CDNs para entrega de anúncios CRS {#multiple-cdn-support-for-crs-ad-delivery}

Embora o cenário padrão do serviço de reempacotamento criativo (CRS) seja usar uma Rede de entrega de conteúdo (CDN), você pode implantar ativos de CRS em mais de uma CDN.

## Requisitos

Você pode usar vários CDNs pelos seguintes motivos:

* Um requisito para escalar para eventos de exibição grandes
* Um requisito para corresponder a origem CDN do ativo CRS à origem CDN do conteúdo principal.
* Um requisito para usar um CDN diferente do CDN padrão do CRS (Akamai).

Quando o servidor de manifesto faz uma pesquisa por solicitações transcodificadas, ele usa um URL de inicialização que contém vários parâmetros de consulta. Se você tiver configurado um ambiente com várias CDNs, o URL de inicialização também precisará conter a variável `ptcdn` parâmetro. O servidor de manifesto usa esse parâmetro para identificar o servidor CDN a partir do qual a versão transcodificada do anúncio será obtida.

Para obter mais detalhes, consulte [Suporte a vários CDNs](../../~old-creative-repackaging-service/multi-cdn-supportt.md) na documentação CRS.
