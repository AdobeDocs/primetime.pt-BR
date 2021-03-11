---
title: Regras de uso
description: Regras de uso
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Regras de uso{#usage-rules}

Com o Adobe Access Server for Protected Streaming, todas as regras de uso são especificadas no servidor por meio de arquivos de configuração. Quaisquer regras de uso especificadas no conteúdo protegido são substituídas, portanto, é recomendável usar uma política anônima simples durante a embalagem do conteúdo. As regras de uso configuráveis podem ser definidas com base no locatário.

O Adobe Access Server for Protected Streaming oferece suporte às seguintes regras de uso:

* Proteção de saída
* Restrições de aplicativos Adobe® AIR®, SWF, iOS e Android
* DRM e restrições do módulo de tempo de execução
* Aplicação da detecção de quebra de martelo (em plataformas de acesso Adobe que suportam a detecção de quebra de martelo)
* O Cache de Licenças é desativado por padrão. O armazenamento em cache de licenças pode ser ativado especificando a data de término do armazenamento em cache ou uma quantidade de tempo permitida (começando quando a licença é emitida).
* Vários direitos de reprodução, que permitem especificar diferentes combinações de Proteção de saída, Restrições de aplicativo e Restrições de DRM/tempo de execução. Por exemplo, é possível especificar diferentes requisitos de Proteção de Saída para cada plataforma cliente usando a Restrição de Módulo DRM com Proteção de Saída.

>[!NOTE]
>
>Para oferecer suporte à entrega remota de chaves para dispositivos iOS, a política usada no momento do empacotamento deve ter a entrega remota de chaves habilitada. Essa configuração não pode ser modificada por meio da configuração do locatário no servidor. ***A Adobe Primetime é necessária para criar aplicativos iOS que possam reproduzir conteúdo protegido por Adobe Access.***

