---
description: Vários CDN permitem que a configuração de um ou mais locais de CDN sirva anúncios transcodificados.
seo-description: Vários CDN permitem que a configuração de um ou mais locais de CDN sirva anúncios transcodificados.
seo-title: Suporte a vários CDN
title: Suporte a vários CDN
uuid: 2b6d71f0-61c8-486b-a35a-f7ef3a9519d2
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff

---


# Suporte a vários CDN {#multi-cdn-support}

Vários CDN permitem que a configuração de um ou mais locais de CDN sirva anúncios transcodificados.

Por padrão, todos os ativos transcodificados são hospedados no Akamai CDN, de propriedade da Adobe. No entanto, você pode escolher zero ou mais locais CDN adicionais de sua propriedade, onde o CRS hospedará o ativo transcodificado. Assim, neste caso, seus ativos e conteúdo transcodificados podem ser servidos a partir do mesmo CDN.

Quando o servidor manifest faz uma pesquisa para solicitações transcodificadas, ele usa um URL de inicialização que contém vários parâmetros de consulta. Se você tiver configurado um ambiente de vários CDN, o URL de inicialização também precisará conter o `ptcdn` parâmetro. O servidor manifest usa esse parâmetro para identificar o servidor CDN do qual obter a versão transcodificada do anúncio.

O suporte a vários CDN também está disponível para as seguintes soluções Primetime:

1. TVSDK para Android
1. TVSDK para HLS de desktop
1. TVSDK para iOS

## Habilitar suporte a CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

Por padrão, o CRS é desativado para todos os clientes

Entre em contato com o gerente técnico de conta da Adobe para configurar sua conta CRS para usar outros CDNs para hospedar os ativos de anúncio transcodificados.Você deverá fornecer as seguintes informações necessárias ao CRS para fazer upload dos ativos de anúncio transcodificados para o CDN

1. URL CDN
1. Detalhes de autenticação
1. Formato de URL de saída

Além disso, seu gerente técnico de conta da Adobe fornecerá um apelido para esta CDN. Você precisa passar esse nome como o valor do `ptcdn` parâmetro no URL do Bootstrap.

Você pode ter várias CDNs configuradas no fim do CRS por meio do suporte da Adobe. No entanto, o CDN usado para selecionar ativos de publicidade a serem suturados pelo servidor manifest precisaria ser aquele transmitido como o valor do `ptcdn` parâmetro no URL do Bootstrap.
