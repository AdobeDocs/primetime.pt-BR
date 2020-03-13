---
description: Com o Adobe Primetime DRM Server for Protected Streaming, você pode especificar todas as regras de uso no servidor com arquivos de configuração.
seo-description: Com o Adobe Primetime DRM Server for Protected Streaming, você pode especificar todas as regras de uso no servidor com arquivos de configuração.
seo-title: Sobre regras de uso
title: Sobre regras de uso
uuid: 4a794712-db58-43f5-b867-8871e58e12ae
translation-type: tm+mt
source-git-commit: 68f1318db89cf9422f5969f669c11f3784560db6

---


# Sobre regras de uso{#about-usage-rules}

Com o Adobe Primetime DRM Server for Protected Streaming, você pode especificar todas as regras de uso no servidor com arquivos de configuração.

Todas as regras de uso especificadas na política DRM para o conteúdo protegido são substituídas. Portanto, a Adobe recomenda que você use uma política DRM simples e anônima durante o empacotamento de conteúdo. Qualquer regra de uso que você pode configurar pode ser configurada por locatário.

O Primetime DRM Server for Protected Streaming oferece suporte às seguintes regras de uso:

* Proteção de saída
* Restrições de aplicativos do Adobe® AIR®, SWF, iOS e Android
* Restrições de módulo de tempo de execução e DRM
* Aplicação de detecção de quebra de falhas em plataformas DRM Primetime que suportam detecção de quebra de carga
* O Cache de Licenças está desativado por padrão. Armazenamento de licenças em cache que você pode ativar especificando a data de término do armazenamento em cache ou uma quantidade de tempo em cache permitida; começa no momento da emissão da licença.
* Vários direitos de reprodução que permitem especificar diferentes combinações de Proteção de saída, Restrições de aplicativo e Restrições de DRM/tempo de execução. Por exemplo, você pode especificar diferentes requisitos de Proteção de saída para cada plataforma cliente usando a Restrição de módulo DRM com Proteção de saída.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Se você quiser oferecer suporte à entrega de chave remota para dispositivos iOS, a política de DRM aplicada no momento do empacotamento deverá ter a entrega de chave remota ativada. Essa configuração não pode ser modificada por meio da configuração do locatário no servidor.

