---
title: Regras de uso
description: Regras de uso
copied-description: true
exl-id: 0f6df09f-47fd-4a05-bcb0-786beaba325a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Regras de uso{#usage-rules}

Com o Adobe Access Server para transmissão protegida, todas as regras de uso são especificadas no servidor por meio de arquivos de configuração. Quaisquer regras de uso especificadas no conteúdo protegido são substituídas, portanto, é recomendável usar uma política anônima simples durante o empacotamento do conteúdo. As regras de uso configuráveis podem ser definidas por locatário.

O Adobe Access Server para transmissão protegida é compatível com as seguintes regras de uso:

* Proteção de saída
* Restrições de aplicativos para Adobe® AIR®, SWF, iOS e Android
* Restrições de DRM e Módulo de Tempo de Execução
* Imposição de detecção de jailbreak (em plataformas de Acesso Adobe que oferecem suporte à detecção de jailbreak)
* O License Caching está desativado por padrão. O armazenamento em cache de licenças pode ser ativado especificando a data final do armazenamento em cache ou uma quantidade de tempo que o armazenamento em cache é permitido (começando quando a licença é emitida).
* Vários direitos de reprodução, que permitem especificar diferentes combinações de Proteção de saída, Restrições de aplicativo e Restrições de DRM/Runtime. Por exemplo, é possível especificar diferentes requisitos de Proteção de Saída para cada plataforma cliente usando a Restrição do Módulo DRM com Proteção de Saída.

>[!NOTE]
>
>Para suportar a entrega remota de chaves para dispositivos iOS, a política usada no momento do empacotamento deve ter a entrega remota de chaves ativada. Esta configuração não pode ser modificada por meio da configuração do locatário no servidor. ***O Adobe Primetime é necessário para criar aplicativos iOS que possam reproduzir conteúdo protegido contra acesso ao Adobe.***
