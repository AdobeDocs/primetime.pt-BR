---
title: Examinando conteúdo de arquivo criptografado
description: Examinando conteúdo de arquivo criptografado
copied-description: true
exl-id: a8a61d1c-c259-4346-9a71-6741f70697ae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Examinando conteúdo de arquivo criptografado {#examining-encrypted-file-content}

Para examinar o conteúdo de um arquivo FLV ou F4V usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em [Configuração do ambiente de desenvolvimento](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) no seu projeto.
1. Criar um `MediaEncrypter` instância.
1. Transmita o arquivo criptografado para o `MediaEncrypter.examineEncryptedContent` método, que retorna um `KeyMetaData` objeto.
1. Inspect as informações contidas no `KeyMetaData` objeto.

Para obter exemplos de código demonstrando como extrair metadados DRM de um arquivo criptografado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` no diretório &quot;samples&quot; de Ferramentas de linha de comando de implementação de referência.
