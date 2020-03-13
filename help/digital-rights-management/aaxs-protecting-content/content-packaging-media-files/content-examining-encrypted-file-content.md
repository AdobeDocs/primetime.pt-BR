---
seo-title: Examinando conteúdo de arquivo criptografado
title: Examinando conteúdo de arquivo criptografado
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Examinando conteúdo de arquivo criptografado {#examining-encrypted-file-content}

Para examinar o conteúdo de um arquivo FLV ou F4V usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em [Configurar o ambiente](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) de desenvolvimento dentro do projeto.
1. Crie uma `MediaEncrypter` instância.
1. Passe o arquivo criptografado para o `MediaEncrypter.examineEncryptedContent` método, que retorna um `KeyMetaData` objeto.
1. Inspecione as informações dentro do `KeyMetaData` objeto.

Para obter um exemplo de código que demonstra como extrair metadados DRM de um arquivo criptografado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` o diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência.
