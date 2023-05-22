---
description: Qualquer uso do Adobe Access consiste em duas etapas principais em pontos diferentes do fluxo de trabalho. A preparação do conteúdo deve ser feita uma vez por ativo e resulta na criação de conteúdo protegido. A aquisição de conteúdo é feita várias vezes, uma para cada consumidor que deseja assistir a esse ativo protegido.
title: Preparação de conteúdo
exl-id: c658c7e9-2583-4d74-a94b-800023cf5196
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Preparação de conteúdo {#content-preparation}

Qualquer uso do Adobe Access consiste em duas etapas principais em pontos diferentes do fluxo de trabalho. A preparação do conteúdo deve ser feita uma vez por ativo e resulta na criação de conteúdo protegido. A aquisição de conteúdo é feita várias vezes, uma para cada consumidor que deseja assistir a esse ativo protegido.

Antes de disponibilizar o conteúdo para distribuição, primeiro você deve codificar o conteúdo no formato de vídeo FLV ou F4V, criar uma ou mais políticas especificando regras de uso para o conteúdo e empacotar o conteúdo usando o SDK do Adobe Access.

As etapas para codificar, empacotar e distribuir conteúdo são as seguintes:

1. Codifique o conteúdo no formato FLV ou F4V usando ferramentas de codificação disponíveis no Adobe ou de terceiros.
1. Crie políticas especificando as regras de uso sob as quais os consumidores podem exibir o conteúdo.

   Uma política é o contêiner das regras e restrições que determinam como, quando e onde o conteúdo protegido pode ser visualizado pelos consumidores.

   O empacotador requer pelo menos uma política com pelo menos uma regra de uso. Você pode substituir a regra de uso e adicionar outras regras de uso quando o License Server gerar a licença.

1. Empacotar o conteúdo e especificar quais políticas aplicar.

   O SDK de acesso do Adobe criptografa o conteúdo usando uma Chave de criptografia de conteúdo (CEK) e vincula uma ou mais políticas ao conteúdo. O resultado é um *arquivo de conteúdo protegido *que só pode ser reproduzido por um consumidor que obteve uma licença do License Server correspondente.

   Durante o empacotamento, o conteúdo é criptografado usando o CEK. O CEK é criptografado usando a chave pública do License Server e incluído nos metadados de DRM junto com as políticas. Os metadados de DRM são assinados usando a chave privada do Packager e os metadados são incluídos no conteúdo protegido.

1. Disponibilizar o conteúdo protegido para distribuição aos consumidores.

   O conteúdo protegido normalmente é distribuído usando uma rede de distribuição de conteúdo (CDN). A CDN pode usar qualquer mecanismo compatível com o tempo de execução do cliente, como Flash Media Server, Adobe HTTP Dynamic Streaming para transmissão de várias taxas de bits ou um servidor Web HTTP para download progressivo.
