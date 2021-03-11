---
title: Examinar conteúdo de arquivo criptografado
description: Examinar conteúdo de arquivo criptografado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Examinar conteúdo de arquivo criptografado{#examining-encrypted-file-content}

Você pode examinar o conteúdo de um arquivo de mídia criptografado usando a API do Java.

Para examinar o conteúdo do arquivo criptografado:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR. Consulte *Configuração do SDK* para seu projeto.
1. Crie uma instância `MediaEncrypter`.
1. Passe o arquivo criptografado para o método `MediaEncrypter.examineEncryptedContent`, que retorna um objeto `KeyMetaData`.

1. Inspect as informações no objeto `KeyMetaData` .

Para obter um código de amostra que descreve como extrair metadados de DRM de um arquivo criptografado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` no diretório Ferramentas de linha de comando de implementação de referência [!DNL samples/] .
