---
title: Licenças pré-geradas
description: Licenças pré-geradas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Licenças pré-geradas{#pre-generating-licenses}

Para pré-gerar licenças, use `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obter uma instância de `LicenseFactory`. Uma credencial de Servidor de Licenças deve ser especificada para assinar as licenças geradas por esta fábrica. Esta classe dá suporte à geração de licenças Leaf sem encadeamento de licenças e de licenças Leaf e Root com o [Encadeamento de licenças aprimorado](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Ao gerar uma licença Leaf, os metadados do conteúdo devem ser especificados usando `initContentInfo()`. Se os metadados incluírem várias políticas ou se você quiser usar uma política que não estava nos metadados, use `setSelectedPolicy()` para especificar a política a ser usada para gerar a licença. Se você usar uma Lista de atualização de política para rastrear atualizações de políticas, poderá fornecer a Lista de atualização de política ao License Fatory antes de inicializar os metadados usando `setPolicyUpdateList()`.

Ao gerar uma licença Raiz, os metadados do conteúdo podem ser especificados conforme descrito acima. Como alternativa, uma licença Raiz pode ser gerada usando uma política ( `setSelectedPolicy()`) e o URL do servidor de licenças ( `setLicenseServerURL()`) em vez dos metadados.

>[!NOTE]
>
>Um URL do License Server é necessário, mesmo que não haja um Adobe Access License Server do qual os clientes possam solicitar uma licença. Nesse caso, o URL do License Server deve especificar um URL que identifique o emissor da licença.

Se a política usar Encadeamento de Licenças Aprimorado, uma credencial do Servidor de Licenças deverá ser especificada para descriptografar a Chave de Criptografia Raiz na política ( `setRootKeyRetrievalInfo()`).

Se a política exigir uma licença associada ao domínio, use `setDomainCAs()` para especificar os emissores de Domínio a partir dos quais o servidor de licenças aceitará tokens de domínio. Um ou mais certificados da autoridade de certificação de domínio devem ser fornecidos para validar o destinatário da licença.

Se a política exigir a entrega remota de chaves para dispositivos iOS, o Certificado do Servidor de Chaves deverá ser fornecido usando `setKeyServerCertificate()`, a menos que uma folha encadeada esteja sendo gerada.

Para gerar uma licença, chame `generateLicense()` e especifique o tipo de licença (Folha ou Raiz) e um ou mais certificados de recipient. O certificado do destinatário será um certificado de computador ou um certificado de domínio, dependendo dos requisitos especificados na política. Se você estiver gerando uma Folha encadeada, um destinatário não será necessário. Após a geração da licença, é possível substituir as regras de uso especificadas na política. Finalmente, chame `signLicense()` para assinar a licença e obter uma instância de `PreGeneratedLicense`. A licença agora pode ser salva em um arquivo (use `getBytes()` para recuperar a licença serializada) ou incorporada ao conteúdo criptografado. Consulte [Incorporação de licenças](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Para obter o código de amostra que demonstra as licenças pré-geradas, consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` no diretório &quot;samples&quot; de Ferramentas de linha de comando de implementação de referência.
