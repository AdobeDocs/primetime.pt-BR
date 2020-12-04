---
description: Embora o cenário padrão do serviço de reempacotamento de criação (CRS) seja o de usar uma Rede de Delivery de Conteúdo (CDN), você pode implantar ativos CRS em mais de um CDN.
seo-description: Embora o cenário padrão do serviço de reempacotamento de criação (CRS) seja o de usar uma Rede de Delivery de Conteúdo (CDN), você pode implantar ativos CRS em mais de um CDN.
seo-title: Suporte a vários CDNs para CRS e delivery
title: Suporte a vários CDNs para CRS e delivery
uuid: c5557a38-aa49-4161-bb58-3e8dff9a4d64
translation-type: tm+mt
source-git-commit: f327b45de7e482dcb25407659846b2098f1fd49d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Suporte a vários CDN para delivery de anúncio CRS {#multiple-cdn-support-for-crs-ad-delivery}

Embora o cenário padrão do serviço de reempacotamento de criação (CRS) seja o de usar uma Rede de Delivery de Conteúdo (CDN), você pode implantar ativos CRS em mais de um CDN.

## Requisitos

Você pode usar várias CDNs pelos seguintes motivos:

* Um requisito para aumentar a escala para eventos de visualização grandes
* Um requisito para corresponder a fonte CDN do ativo CRS à fonte CDN do conteúdo principal.
* Um requisito para usar um CDN diferente do CDN padrão do CRS (Akamai).

Quando o servidor manifest faz uma pesquisa para solicitações transcodificadas, ele usa um URL de inicialização que contém vários parâmetros de query. Se você tiver configurado um ambiente de vários CDN, o URL de inicialização também precisará conter o parâmetro `ptcdn`. O servidor manifest usa esse parâmetro para identificar o servidor CDN do qual obter a versão transcodificada do anúncio.

Para obter mais detalhes, consulte [Suporte a vários CDN](../../creative-repackaging-service/multi-cdn-supportt.md) na documentação do CRS.
