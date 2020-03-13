---
seo-title: Examinando conteúdo de arquivo criptografado
title: Examinando conteúdo de arquivo criptografado
uuid: 1b3318f6-0850-43f2-9127-c72ea81a1bdf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Examinando conteúdo de arquivo criptografado{#examining-encrypted-file-content}

Você pode examinar o conteúdo de um arquivo de mídia criptografado usando a API Java.

Para examinar o conteúdo do arquivo criptografado:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR. Consulte *Configuração do SDK* para seu projeto.
1. Crie uma `MediaEncrypter` instância.
1. Passe o arquivo criptografado para o `MediaEncrypter.examineEncryptedContent` método, que retorna um `KeyMetaData` objeto.

1. Inspecione as informações dentro do `KeyMetaData` objeto.

Para obter um exemplo de código que descreve como extrair metadados DRM de um arquivo criptografado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` o diretório Ferramentas de Linha de Comando de Implementação de Referência [!DNL samples/] .
