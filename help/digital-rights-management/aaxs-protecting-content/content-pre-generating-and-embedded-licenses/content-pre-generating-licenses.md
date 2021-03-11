---
title: Licenças pré-geradoras
description: Licenças pré-geradoras
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Licenças pré-geradoras{#pre-generating-licenses}

Para pré-gerar licenças, use `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obter uma instância de `LicenseFactory`. É necessário especificar uma credencial do License Server para assinar as licenças geradas por esta fábrica. Esta classe suporta a geração de licenças Folha sem licença de cadeia e licenças Folha e Raiz com o [Encadeamento de licença Avançado](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Ao gerar uma licença do Folha, os metadados de conteúdo devem ser especificados usando `initContentInfo()`. Se os metadados incluírem várias políticas, ou se você quiser usar uma política que não estava nos metadados, use `setSelectedPolicy()` para especificar a política a ser usada para gerar a licença. Se você usar uma Lista de Atualização de Política para rastrear atualizações de políticas, poderá fornecer a Lista de Atualização de Política para a Fábrica de Licenças antes de inicializar os metadados usando `setPolicyUpdateList()`.

Ao gerar uma licença de Raiz, os metadados de conteúdo podem ser especificados conforme descrito acima. Como alternativa, uma licença Raiz pode ser gerada usando uma política ( `setSelectedPolicy()`) e o URL do servidor de licença ( `setLicenseServerURL()`) em vez dos metadados.

>[!NOTE]
>
>Um URL do License Server é necessário mesmo se não houver um Adobe Access License Server do qual os clientes possam solicitar uma licença. Nesse caso, o URL do License Server deve especificar um URL que identifique o emissor da licença.

Se a política usar o Encadeamento de Licenças Avançado, uma credencial do License Server deverá ser especificada para descriptografar a Chave de Criptografia Raiz na política ( `setRootKeyRetrievalInfo()`).

Se a política exigir uma licença vinculada ao domínio, use `setDomainCAs()` para especificar os emissores de domínio dos quais o servidor de licença aceitará tokens de domínio. Um ou mais certificados de autoridade de certificação de domínio devem ser fornecidos para validar o destinatário da licença.

Se a política exigir a entrega remota de chaves para dispositivos iOS, o Certificado de Servidor de Chave deve ser fornecido usando `setKeyServerCertificate()`, a menos que uma Folha de Chave esteja sendo gerada.

Para gerar uma licença, chame `generateLicense()` e especifique o tipo de licença (Folha ou Raiz) e um ou mais certificados de recipient. O certificado do recipient será um certificado de máquina ou de domínio, dependendo dos requisitos especificados na política. Se você estiver gerando uma Folha encadeada, um recipient não será necessário. Após a licença ter sido gerada, é possível substituir as regras de uso especificadas na política. Finalmente, chame `signLicense()` para assinar a licença e obter uma instância de `PreGeneratedLicense`. A licença agora pode ser salva em um arquivo (use `getBytes()` para recuperar a licença serializada) ou incorporada ao conteúdo criptografado. Consulte, [Incorporando licenças](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Para obter um código de amostra demonstrando licenças pré-geradas, consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` no diretório &quot;samples&quot; de Ferramentas de Linha de Comando de Implementação de Referência.
