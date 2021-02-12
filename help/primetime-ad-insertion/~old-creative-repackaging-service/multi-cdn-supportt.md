---
description: Vários CDN permitem que a configuração de um ou mais locais de CDN sirva anúncios transcodificados.
seo-description: Vários CDN permitem que a configuração de um ou mais locais de CDN sirva anúncios transcodificados.
seo-title: Suporte a vários CDN
title: Suporte a vários CDN
uuid: 2b6d71f0-61c8-486b-a35a-f7ef3a9519d2
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Suporte a vários CDN {#multi-cdn-support}

Vários CDN permitem que a configuração de um ou mais locais de CDN sirva anúncios transcodificados.

Por padrão, todos os ativos transcodificados são hospedados na Akamai CDN de propriedade do Adobe. No entanto, você pode escolher zero ou mais locais CDN adicionais de sua propriedade, onde o CRS hospedará o ativo transcodificado. Assim, neste caso, seus ativos e conteúdo transcodificados podem ser servidos a partir do mesmo CDN.

Quando o servidor manifest faz uma pesquisa para solicitações transcodificadas, ele usa um URL de inicialização que contém vários parâmetros de query. Se você tiver configurado um ambiente de vários CDN, o URL de inicialização também precisará conter o parâmetro `ptcdn`. O servidor manifest usa esse parâmetro para identificar o servidor CDN do qual obter a versão transcodificada do anúncio.

O suporte a vários CDN também está disponível para as seguintes soluções Primetime:

1. TVSDK para Android
1. TVSDK para HLS de desktop
1. TVSDK para iOS

## Habilitar suporte a CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

Por padrão, o CRS é desativado para todos os clientes

Entre em contato com o gerente técnico de conta do Adobe para configurar sua conta CRS para usar outros CDNs para hospedar os ativos de anúncio transcodificados.Você deverá fornecer as seguintes informações necessárias ao CRS para fazer upload dos ativos de anúncio transcodificados para o CDN

1. URL CDN
1. Detalhes de autenticação
1. Formato de URL de saída

Além disso, seu gerente técnico de conta do Adobe fornecerá um apelido para este CDN.Você precisa passar isso como o valor do parâmetro `ptcdn` no URL do Bootstrap.

É possível ter várias CDNs configuradas no fim do CRS por meio do suporte ao Adobe. No entanto, o CDN usado para selecionar ativos de publicidade a serem associados pelo servidor manifest precisaria ser aquele que é transmitido como o valor do parâmetro `ptcdn` no URL do Bootstrap.