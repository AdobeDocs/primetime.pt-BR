---
seo-title: Regras de uso
title: Regras de uso
uuid: 361d07b9-e4c8-47ab-8c45-a1de98c9fed7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Regras de uso{#usage-rules}

Com o Adobe Access Server for Protected Streaming, todas as regras de uso são especificadas no servidor por meio de arquivos de configuração. Todas as regras de uso especificadas no conteúdo protegido são substituídas, portanto, é recomendável usar uma política anônima simples durante o empacotamento do conteúdo. As regras de uso configuráveis podem ser definidas por locatário.

O Adobe Access Server for Protected Streaming oferece suporte às seguintes regras de uso:

* Proteção de saída
* Restrições de aplicativos do Adobe® AIR®, SWF, iOS e Android
* Restrições de módulo de tempo de execução e DRM
* Aplicação da detecção de quebra de carga (em plataformas do Adobe Access que suportam detecção de quebra de prisão)
* O Cache de Licenças está desativado por padrão. O cache de licenças pode ser ativado especificando a data de término do armazenamento em cache ou um tempo em cache permitido (a partir do momento em que a licença é emitida).
* Vários direitos de reprodução, que permitem especificar diferentes combinações de Proteção de saída, Restrições de aplicativo e Restrições de DRM/tempo de execução. Por exemplo, é possível especificar diferentes requisitos de Proteção de saída para cada plataforma cliente usando a Restrição de módulo DRM com Proteção de saída.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Para suportar a entrega de chave remota para dispositivos iOS, a política usada no momento do empacotamento deve ter a entrega de chave remota ativada. Essa configuração não pode ser modificada por meio da configuração do locatário no servidor. ***O Adobe Primetime é necessário para criar aplicativos iOS que podem reproduzir conteúdo protegido pelo Adobe Access.***

