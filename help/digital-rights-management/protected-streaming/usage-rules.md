---
description: Com o servidor DRM da Adobe Primetime para transmissão protegida, você pode especificar todas as regras de uso no servidor com arquivos de configuração.
title: Sobre as regras de uso
exl-id: 55af3a18-8fdb-4285-bd9f-ca479475e34f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Sobre as regras de uso{#about-usage-rules}

Com o servidor DRM da Adobe Primetime para transmissão protegida, você pode especificar todas as regras de uso no servidor com arquivos de configuração.

Quaisquer regras de uso especificadas na política DRM para o conteúdo protegido são substituídas. Portanto, a Adobe recomenda o uso de uma política de DRM simples e anônima durante o empacotamento do conteúdo. Todas as regras de uso que você pode configurar podem ser configuradas com base no locatário.

O Servidor DRM do Primetime para Transmissão Protegida aceita as seguintes regras de uso:

* Proteção de saída
* Restrições de aplicativos para Adobe® AIR®, SWF, iOS e Android
* Restrições de DRM e Módulo de Tempo de Execução
* Imposição da detecção de jailbreak em plataformas DRM do Primetime que oferecem suporte à detecção de jailbreak
* O License Caching está desativado por padrão. O armazenamento em cache de licenças que você pode habilitar especificando a data final do armazenamento em cache ou uma quantidade de tempo em cache é permitido; ele começa quando a licença é emitida.
* Vários direitos de reprodução que permitem especificar diferentes combinações de Proteção de saída, Restrições de aplicativo e Restrições de DRM/Runtime. Por exemplo, você pode especificar diferentes requisitos de Proteção de Saída para cada plataforma cliente usando a Restrição do Módulo DRM com Proteção de Saída.

>[!NOTE]
>
>Se você quiser oferecer suporte à entrega remota de chaves para dispositivos iOS, a política de DRM aplicada no momento do empacotamento deverá ter a entrega remota de chaves ativada. Esta configuração não pode ser modificada por meio da configuração do locatário no servidor.
