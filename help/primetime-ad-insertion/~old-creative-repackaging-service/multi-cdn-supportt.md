---
description: Multi CDN permite que a configuração de um ou mais locais de CDN sirvam anúncios transcodificados.
title: Suporte a várias CDNs
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Suporte a vários CDN {#multi-cdn-support}

Multi CDN permite que a configuração de um ou mais locais de CDN sirvam anúncios transcodificados.

Por padrão, todos os ativos transcodificados são hospedados no Akamai CDN, de propriedade do Adobe. No entanto, você pode escolher zero ou mais localizações de CDN adicionais da sua conta, onde o CRS hospedará o ativo transcodificado. Portanto, nesse caso, seus ativos e conteúdo transcodificados podem ser distribuídos a partir da mesma CDN.

Quando o servidor manifest faz uma pesquisa de solicitações transcodificadas, ele usa um URL de bootstrap que contém vários parâmetros de consulta. Se você configurou um ambiente de várias CDN, o URL de inicialização também precisará conter o parâmetro `ptcdn`. O servidor de manifesto usa esse parâmetro para identificar o servidor CDN do qual obter a versão transcodificada do anúncio.

O suporte a vários CDN também está disponível para as seguintes soluções do Primetime:

1. TVSDK para Android
1. TVSDK para Desktop HLS
1. TVSDK para iOS

## Habilitar o suporte a CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

Por padrão, o CRS é desativado para todos os clientes

Entre em contato com o gerente técnico de conta do Adobe para configurar a conta do CRS para usar outras CDNs para hospedar os ativos de anúncio transcodificados. Você deverá fornecer as seguintes informações necessárias para que o CRS faça o upload dos ativos de anúncio transcodificados para a CDN

1. URL CDN
1. Detalhes de autenticação
1. Formato do URL de saída

Além disso, seu gerente técnico de conta do Adobe fornecerá um apelido para essa CDN. Você precisa passar isso como o valor do parâmetro `ptcdn` no URL do Bootstrap.

É possível ter várias CDNs configuradas no fim do CRS por meio do Adobe Support. No entanto, a CDN usada para selecionar ativos de anúncio a serem compilados por meio do servidor de manifesto precisaria ser aquela que é passada como o valor do parâmetro `ptcdn` no URL do Bootstrap.
