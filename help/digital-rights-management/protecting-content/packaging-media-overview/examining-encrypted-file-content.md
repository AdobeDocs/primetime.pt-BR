---
title: Examinando conteúdo de arquivo criptografado
description: Examinando conteúdo de arquivo criptografado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Examinando conteúdo de arquivo criptografado{#examining-encrypted-file-content}

Você pode examinar o conteúdo de um arquivo de mídia criptografado usando a API Java.

Para examinar o conteúdo do arquivo criptografado:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR. Consulte *Configuração do SDK* para o seu projeto.
1. Criar um `MediaEncrypter` instância.
1. Transmita o arquivo criptografado para o `MediaEncrypter.examineEncryptedContent` método, que retorna um `KeyMetaData` objeto.

1. Inspect as informações contidas no `KeyMetaData` objeto.

Para obter exemplos de código que descrevem como extrair metadados de DRM de um arquivo criptografado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` nas Ferramentas de linha de comando da Implementação de referência [!DNL samples/] diretório.
