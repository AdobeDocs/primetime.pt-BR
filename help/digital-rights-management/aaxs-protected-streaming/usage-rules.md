---
seo-title: Regras de uso
title: Regras de uso
uuid: 361d07b9-e4c8-47ab-8c45-a1de98c9fed7
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Regras de uso{#usage-rules}

Com o Adobe Access Server for Protected Streaming, todas as regras de uso são especificadas no servidor por meio de arquivos de configuração. Todas as regras de uso especificadas no conteúdo protegido são substituídas, portanto, é recomendável usar uma política anônima simples durante o empacotamento do conteúdo. As regras de uso configuráveis podem ser definidas por locatário.

O Adobe Access Server for Protected Streaming oferece suporte às seguintes regras de uso:

* Proteção de saída
* Restrições de aplicativos Adobe® AIR®, SWF, iOS e Android
* Restrições de módulo de tempo de execução e DRM
* Aplicação da detecção de interrupções (em plataformas de acesso a Adobe que suportam a detecção de parada)
* O Cache de Licenças está desativado por padrão. O cache de licenças pode ser ativado especificando a data de término do armazenamento em cache ou um tempo em cache permitido (a partir do momento em que a licença é emitida).
* Vários direitos de reprodução, que permitem especificar diferentes combinações de Proteção de saída, Restrições de aplicativo e Restrições de DRM/tempo de execução. Por exemplo, é possível especificar diferentes requisitos de Proteção de saída para cada plataforma cliente usando a Restrição de módulo DRM com Proteção de saída.

>[!NOTE]
>
>Para suportar o delivery de chave remota para dispositivos iOS, a política usada no momento do empacotamento deve ter o delivery de chave remota habilitado. Essa configuração não pode ser modificada por meio da configuração do locatário no servidor. ***A Adobe Primetime é necessária para criar aplicativos iOS que possam reproduzir conteúdo protegido pelo Adobe Access.***

