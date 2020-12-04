---
seo-title: Examinando conteúdo de arquivo criptografado
title: Examinando conteúdo de arquivo criptografado
uuid: 1b3318f6-0850-43f2-9127-c72ea81a1bdf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Examinando conteúdo de arquivo criptografado{#examining-encrypted-file-content}

Você pode examinar o conteúdo de um arquivo de mídia criptografado usando a API Java.

Para examinar o conteúdo do arquivo criptografado:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR. Consulte *Configuração do SDK* para o seu projeto.
1. Crie uma instância `MediaEncrypter`.
1. Passe o arquivo criptografado para o método `MediaEncrypter.examineEncryptedContent`, que retorna um objeto `KeyMetaData`.

1. Inspect as informações dentro do objeto `KeyMetaData`.

Para obter um exemplo de código que descreve como extrair metadados DRM de um arquivo criptografado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` no diretório Ferramentas de Linha de Comando de Implementação de Referência [!DNL samples/].
