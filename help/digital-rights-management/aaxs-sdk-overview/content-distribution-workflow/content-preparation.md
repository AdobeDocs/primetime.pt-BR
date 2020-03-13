---
description: Qualquer uso do Adobe Access consiste em duas etapas principais em diferentes pontos do fluxo de trabalho. A preparação de conteúdo deve ser feita uma vez por ativo e resulta na criação de conteúdo protegido. A aquisição de conteúdo é feita várias vezes, uma para todos os consumidores que desejam assistir a esse ativo protegido.
seo-description: Qualquer uso do Adobe Access consiste em duas etapas principais em diferentes pontos do fluxo de trabalho. A preparação de conteúdo deve ser feita uma vez por ativo e resulta na criação de conteúdo protegido. A aquisição de conteúdo é feita várias vezes, uma para todos os consumidores que desejam assistir a esse ativo protegido.
seo-title: Preparação do conteúdo
title: Preparação do conteúdo
uuid: 7a3562c6-6033-4e28-8f0a-18e3cb8987b9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Preparação do conteúdo {#content-preparation}

Qualquer uso do Adobe Access consiste em duas etapas principais em diferentes pontos do fluxo de trabalho. A preparação de conteúdo deve ser feita uma vez por ativo e resulta na criação de conteúdo protegido. A aquisição de conteúdo é feita várias vezes, uma para todos os consumidores que desejam assistir a esse ativo protegido.

Antes de disponibilizar o conteúdo para distribuição, você deve primeiro codificar o conteúdo no formato de vídeo FLV ou F4V, criar uma ou mais políticas que especifiquem as regras de uso do conteúdo e disponibilizar o conteúdo usando o SDK do Adobe Access.

As etapas para codificar, disponibilizar e distribuir conteúdo são as seguintes:

1. Codifique o conteúdo no formato FLV ou F4V usando as ferramentas de codificação disponíveis da Adobe ou de terceiros.
1. Crie políticas que especifiquem as regras de uso nas quais os consumidores podem exibir o conteúdo.

   Uma política é o contêiner das regras e restrições que determinam como, quando e onde o conteúdo protegido pode ser visualizado pelos consumidores.

   O empacotador requer pelo menos uma política com pelo menos uma regra de uso. Você pode substituir a regra de uso e adicionar outras regras de uso quando o License Server gerar a licença.

1. Empacote o conteúdo e especifique as políticas a serem aplicadas.

   O SDK do Adobe Access criptografa o conteúdo usando uma Chave de criptografia de conteúdo (CEK) e vincula uma ou mais políticas ao conteúdo. O resultado é um *arquivo de conteúdo protegido *que só pode ser reproduzido por um consumidor que tenha obtido uma licença do License Server correspondente.

   Durante o empacotamento, o conteúdo é criptografado usando o CEK. O CEK é criptografado usando a chave pública do License Server e incluído nos metadados do DRM juntamente com as políticas. Os metadados DRM são assinados usando a chave privada Packager, e os metadados são incluídos no conteúdo protegido.

1. Disponibilize o conteúdo protegido para distribuição aos consumidores.

   O conteúdo protegido é geralmente distribuído usando uma rede de distribuição de conteúdo (CDN). O CDN pode usar qualquer mecanismo suportado pelo tempo de execução do cliente, como Flash Media Server, Adobe HTTP Dynamic Streaming para vários streaming de taxa de bits ou HTTP Web Server para download progressivo.

