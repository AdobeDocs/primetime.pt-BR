---
description: O Multi CDN permite a configuração de um ou mais locais CDN para veicular anúncios transcodificados.
title: Suporte a vários CDNs
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Suporte a vários CDNs {#multi-cdn-support}

O Multi CDN permite a configuração de um ou mais locais CDN para veicular anúncios transcodificados.

Por padrão, todos os ativos transcodificados são hospedados no Akamai CDN de propriedade do Adobe. No entanto, você pode escolher zero ou mais locais CDN adicionais próprios, onde o CRS hospedará o ativo transcodificado. Portanto, nesse caso, os ativos e o conteúdo transcodificados podem ser fornecidos pela mesma CDN.

Quando o servidor de manifesto faz uma pesquisa por solicitações transcodificadas, ele usa um URL de inicialização que contém vários parâmetros de consulta. Se você tiver configurado um ambiente com várias CDNs, o URL de inicialização também precisará conter a variável `ptcdn` parameter. O servidor de manifesto usa esse parâmetro para identificar o servidor CDN a partir do qual a versão transcodificada do anúncio será obtida.

O suporte a várias CDNs também está disponível para as seguintes soluções do Primetime:

1. TVSDK para Android
1. TVSDK para HLS de desktop
1. TVSDK para iOS

## Habilitar suporte a CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

Por padrão, o CRS é desativado para todos os clientes

Entre em contato com o gerente técnico de conta do Adobe para configurar a conta do CRS para usar outras CDNs para hospedar os ativos de anúncios transcodificados. Você precisará fornecer as seguintes informações, necessárias para que o CRS faça upload dos ativos de anúncios transcodificados para a CDN

1. URL DA CDN
1. Detalhes da autenticação
1. Formato de URL de saída

Além disso, o gerente técnico de conta do Adobe fornecerá um apelido para essa CDN. É necessário passar isso como o valor do `ptcdn` no URL do Bootstrap.

Você pode ter vários CDNs configurados no CRS end via Suporte para Adobe. No entanto, a CDN usada para selecionar ativos de anúncios a serem compilados por meio do servidor de manifesto precisaria ser a que é passada como o valor do `ptcdn` no URL do Bootstrap.
