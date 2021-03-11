---
title: Examinar conteúdo de arquivo criptografado
description: Examinar conteúdo de arquivo criptografado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Examinar conteúdo de arquivo criptografado {#examining-encrypted-file-content}

Para examinar o conteúdo de um arquivo FLV ou F4V usando a API do Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em [Setting up the development environment](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) no seu projeto.
1. Crie uma instância `MediaEncrypter`.
1. Passe o arquivo criptografado para o método `MediaEncrypter.examineEncryptedContent`, que retorna um objeto `KeyMetaData`.
1. Inspect as informações no objeto `KeyMetaData` .

Para obter um código de amostra que demonstra como extrair metadados de DRM de um arquivo criptografado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` no diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência.
