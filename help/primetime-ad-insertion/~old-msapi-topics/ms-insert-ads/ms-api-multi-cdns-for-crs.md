---
description: Embora o cenário padrão do Creative Repackaging Service (CRS) seja usar uma Rede de entrega de conteúdo (CDN), é possível implantar ativos do CRS em mais de uma CDN.
title: Suporte a várias CDNs para entrega de anúncios CRS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Suporte a várias CDNs para entrega de anúncios CRS {#multiple-cdn-support-for-crs-ad-delivery}

Embora o cenário padrão do Creative Repackaging Service (CRS) seja usar uma Rede de entrega de conteúdo (CDN), é possível implantar ativos do CRS em mais de uma CDN.

## Requisitos

Você pode usar vários CDNs pelos seguintes motivos:

* Um requisito para dimensionar para eventos de exibição grandes
* Um requisito para corresponder a fonte CDN do ativo CRS à fonte CDN do conteúdo principal.
* Um requisito para usar um CDN diferente do CDN padrão do CRS (Akamai).

Quando o servidor manifest faz uma pesquisa de solicitações transcodificadas, ele usa um URL de bootstrap que contém vários parâmetros de consulta. Se você configurou um ambiente de várias CDN, o URL de inicialização também precisará conter o parâmetro `ptcdn`. O servidor manifest usa esse parâmetro para identificar o servidor CDN do qual obter a versão transcodificada do anúncio.

Para obter mais detalhes, consulte [Suporte a vários CDN](../../~old-creative-repackaging-service/multi-cdn-supportt.md) na documentação do CRS.
