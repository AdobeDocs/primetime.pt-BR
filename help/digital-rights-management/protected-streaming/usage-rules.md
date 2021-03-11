---
description: Com o Adobe Primetime DRM Server for Protected Streaming, é possível especificar todas as regras de uso no servidor com arquivos de configuração.
title: Sobre regras de uso
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# Sobre as regras de uso{#about-usage-rules}

Com o Adobe Primetime DRM Server for Protected Streaming, é possível especificar todas as regras de uso no servidor com arquivos de configuração.

Quaisquer regras de uso especificadas na política de DRM para o conteúdo protegido são substituídas. Portanto, o Adobe recomenda usar uma política de DRM simples e anônima durante a embalagem do conteúdo. Quaisquer regras de uso que você pode configurar podem ser configuradas por locatário.

O servidor DRM Primetime para transmissão protegida oferece suporte às seguintes regras de uso:

* Proteção de saída
* Restrições de aplicativos Adobe® AIR®, SWF, iOS e Android
* DRM e restrições do módulo de tempo de execução
* Aplicação de detecção de quebra de martelo em plataformas DRM Primetime que oferecem suporte à detecção de quebra de maré
* O Cache de Licenças é desativado por padrão. Cache de licenças que você pode ativar especificando a data de término do armazenamento em cache ou uma quantidade de tempo em cache permitida; começa a partir da emissão do certificado.
* Vários Direitos de Reprodução que permitem especificar diferentes combinações de Proteção de Saída, Restrições de Aplicativo e Restrições de DRM/Tempo de Execução. Por exemplo, você pode especificar diferentes requisitos de Proteção de Saída para cada plataforma de cliente usando a Restrição de Módulo DRM com Proteção de Saída.

>[!NOTE]
>
>Se você quiser oferecer suporte à entrega remota de chaves para dispositivos iOS, a política de DRM aplicada no momento da embalagem deverá ter a entrega remota de chaves ativada. Essa configuração não pode ser modificada por meio da configuração do locatário no servidor.

