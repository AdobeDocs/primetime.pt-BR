---
seo-title: Licenças pré-geradoras
title: Licenças pré-geradoras
uuid: 31430753-11f1-4ce5-b402-cf4279119a05
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Licenças pré-geradoras{#pre-generating-licenses}

Para pré-gerar licenças, use `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obter uma instância de `LicenseFactory`. É necessário especificar uma credencial do License Server para assinar as licenças geradas por esta fábrica. Esta classe suporta a geração de licenças Leaf sem encadeamento de licença e licenças Leaf e Root com encadeamento de licença [Enhanced](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Ao gerar uma licença Folha, os metadados do conteúdo devem ser especificados usando `initContentInfo()`. Se os metadados incluírem várias políticas, ou se você quiser usar uma política que não esteja nos metadados, use `setSelectedPolicy()` para especificar a política a ser usada para gerar a licença. Se você usar uma Lista de Atualização de política para rastrear atualizações de políticas, poderá fornecer a Lista de Atualização de política para o Fábrica de licenças antes de inicializar os metadados usando `setPolicyUpdateList()`.

Ao gerar uma licença raiz, os metadados do conteúdo podem ser especificados como descrito acima. Como alternativa, uma licença raiz pode ser gerada usando uma política ( `setSelectedPolicy()`) e o URL do servidor de licença ( `setLicenseServerURL()`) em vez dos metadados.

>[!NOTE]
>
>Um URL do License Server é necessário mesmo se não houver um Adobe Access License Server do qual os clientes possam solicitar uma licença. Nesse caso, o URL do License Server deve especificar um URL que identifique o emissor da licença.

Se a política usar o Encadeamento aprimorado de licença, uma credencial do License Server deverá ser especificada para descriptografar a chave de criptografia raiz na política ( `setRootKeyRetrievalInfo()`).

Se a política exigir uma licença vinculada ao domínio, use `setDomainCAs()` para especificar os emissores de domínio dos quais o servidor de licença aceitará tokens de domínio. É necessário fornecer um ou mais certificados de CA de domínio para validar o recipient de licença.

Se a política exigir delivery de chave remota para dispositivos iOS, o Certificado de Servidor de Chave deverá ser fornecido usando `setKeyServerCertificate()`, a menos que uma Folha Cadeada esteja sendo gerada.

Para gerar uma licença, chame `generateLicense()` e especifique o tipo de licença (Folha ou Raiz) e um ou mais certificados de recipient. O certificado de recipient será um certificado de computador ou de domínio, dependendo dos requisitos especificados na política. Se você estiver gerando uma Folha acorrentada, um recipient não é obrigatório. Depois que a licença é gerada, é possível substituir as regras de uso especificadas na política. Finalmente, invoque `signLicense()` para assinar a licença e obter uma instância de `PreGeneratedLicense`. A licença agora pode ser salva em um arquivo (use `getBytes()` para recuperar a licença serializada) ou incorporada em conteúdo criptografado. Consulte, [Incorporando Licenças](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Para obter exemplos de códigos que demonstram licenças pré-geradas, consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` o diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência.
