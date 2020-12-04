---
description: Com o Adobe Primetime DRM Server for Protected Streaming, você pode especificar todas as regras de uso no servidor com arquivos de configuração.
seo-description: Com o Adobe Primetime DRM Server for Protected Streaming, você pode especificar todas as regras de uso no servidor com arquivos de configuração.
seo-title: Sobre regras de uso
title: Sobre regras de uso
uuid: 4a794712-db58-43f5-b867-8871e58e12ae
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Sobre as regras de uso{#about-usage-rules}

Com o Adobe Primetime DRM Server for Protected Streaming, você pode especificar todas as regras de uso no servidor com arquivos de configuração.

Todas as regras de uso especificadas na política DRM para o conteúdo protegido são substituídas. Portanto, o Adobe recomenda que você use uma política DRM simples e anônima durante o empacotamento de conteúdo. Qualquer regra de uso que você pode configurar pode ser configurada por locatário.

O Primetime DRM Server for Protected Streaming oferece suporte às seguintes regras de uso:

* Proteção de saída
* Restrições de aplicativos Adobe® AIR®, SWF, iOS e Android
* Restrições de módulo de tempo de execução e DRM
* Aplicação de detecção de quebra de falhas em plataformas DRM Primetime que suportam detecção de quebra de carga
* O Cache de Licenças está desativado por padrão. Armazenamento de licenças em cache que você pode ativar especificando a data de término do armazenamento em cache ou uma quantidade de tempo em cache permitida; start quando a licença é emitida.
* Vários direitos de reprodução que permitem especificar diferentes combinações de Proteção de saída, Restrições de aplicativo e Restrições de DRM/tempo de execução. Por exemplo, você pode especificar diferentes requisitos de Proteção de saída para cada plataforma cliente usando a Restrição de módulo DRM com Proteção de saída.

>[!NOTE]
>
>Se você quiser oferecer suporte ao delivery de chave remota para dispositivos iOS, a política de DRM aplicada no momento do empacotamento deverá ter o delivery de chave remota habilitado. Essa configuração não pode ser modificada por meio da configuração do locatário no servidor.

