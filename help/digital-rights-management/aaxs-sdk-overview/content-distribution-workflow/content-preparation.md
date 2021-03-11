---
description: Qualquer uso do Acesso ao Adobe consiste em duas etapas principais em pontos diferentes do fluxo de trabalho. A preparação do conteúdo deve ser feita uma vez por ativo e resulta na criação de conteúdo protegido. A aquisição de conteúdo é feita várias vezes, uma para cada consumidor que deseja assistir a esse ativo protegido.
title: Preparação do conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# Preparação de conteúdo {#content-preparation}

Qualquer uso do Acesso ao Adobe consiste em duas etapas principais em pontos diferentes do fluxo de trabalho. A preparação do conteúdo deve ser feita uma vez por ativo e resulta na criação de conteúdo protegido. A aquisição de conteúdo é feita várias vezes, uma para cada consumidor que deseja assistir a esse ativo protegido.

Antes de disponibilizar conteúdo para distribuição, primeiro você deve codificar o conteúdo no formato de vídeo FLV ou F4V, criar uma ou mais políticas especificando regras de uso para o conteúdo e empacotar o conteúdo usando o SDK do Adobe Access.

As etapas para codificar, empacotar e distribuir conteúdo são as seguintes:

1. Codifique o conteúdo no formato FLV ou F4V usando ferramentas de codificação disponíveis no Adobe ou de terceiros.
1. Crie políticas especificando as regras de uso nas quais os consumidores podem visualizar o conteúdo.

   Uma política é o contêiner das regras e restrições que determinam como, quando e onde o conteúdo protegido pode ser visualizado pelos consumidores.

   O empacotador requer pelo menos uma política com pelo menos uma regra de uso. Você pode substituir a regra de uso e adicionar regras de uso adicionais quando o License Server gerar a licença.

1. Comprima o conteúdo e especifique as políticas a serem aplicadas.

   O SDK de acesso ao Adobe criptografa o conteúdo usando uma Chave de criptografia de conteúdo (CEK) e vincula uma ou mais políticas ao conteúdo. O resultado é um *arquivo de conteúdo protegido *que só pode ser reproduzido por um consumidor que tenha obtido uma licença do License Server correspondente.

   Durante a embalagem, o conteúdo é criptografado usando o CEK. O CEK é criptografado usando a chave pública do License Server e incluído nos metadados do DRM junto com as políticas. Os metadados de DRM são assinados usando a chave privada do Packager e os metadados são incluídos no conteúdo protegido.

1. Disponibilizar o conteúdo protegido para distribuição aos consumidores.

   O conteúdo protegido é normalmente distribuído usando uma rede de distribuição de conteúdo (CDN). A CDN pode usar qualquer mecanismo suportado pelo tempo de execução do cliente, como Flash Media Server, Adobe HTTP Dynamic Streaming para streaming de várias taxas de bits ou um Servidor Web HTTP para download progressivo.

