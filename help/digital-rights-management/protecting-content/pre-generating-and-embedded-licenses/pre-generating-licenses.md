---
description: Se você usar o Adobe Primetime DRM Professional, poderá pré-gerar licenças e incorporar licenças no conteúdo. Esse recurso pode ser combinado com o Encadeamento de Licenças Avançado, de modo que uma licença de Folha seja pré-gerada e incorporada no conteúdo, e o cliente possa solicitar uma licença de Raiz (vinculada a uma máquina ou domínio) de um servidor de licença. Como alternativa, os aplicativos clientes podem implementar um fluxo de trabalho em que o dispositivo se registra previamente em um servidor, o servidor gera previamente licenças que são vinculadas a esse dispositivo e o cliente recupera suas licenças de um servidor Web HTTP simples.
title: Licenças pré-geradoras
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# Licenças pré-geradoras {#pre-generating-licenses}

Se você usar o Adobe Primetime DRM Professional, poderá pré-gerar licenças e incorporar licenças no conteúdo. Esse recurso pode ser combinado com o Encadeamento de Licenças Avançado, de modo que uma licença de Folha seja pré-gerada e incorporada no conteúdo, e o cliente possa solicitar uma licença de Raiz (vinculada a uma máquina ou domínio) de um servidor de licença. Como alternativa, os aplicativos clientes podem implementar um fluxo de trabalho em que o dispositivo se registra previamente em um servidor, o servidor gera previamente licenças que são vinculadas a esse dispositivo e o cliente recupera suas licenças de um servidor Web HTTP simples.

Se quiser pré-gerar licenças, você deve usar `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obter uma instância de `LicenseFactory`. Você deve especificar uma credencial do License Server para assinar as licenças geradas por esta fábrica. Esta classe suporta a geração de licenças Folha sem licença de cadeia e licenças Folha e Raiz com o [Encadeamento de licença Avançado](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

Ao gerar uma licença do Folha, você deve especificar os metadados de conteúdo que se aplicam `initContentInfo()`. Se os metadados incluírem várias políticas de DRM, ou se você quiser usar uma política de DRM que não tenha sido incluída nos metadados, deverá usar `setSelectedPolicy()` para especificar a política de DRM para gerar uma licença. Se você usar uma Lista de atualização da política de DRM para rastrear atualizações das políticas de DRM, poderá fornecer a Lista de atualização da política de DRM à Fábrica de licença antes de inicializar os metadados com `setPolicyUpdateList()`.

Ao gerar uma licença Raiz, você deve especificar os metadados de conteúdo conforme descrito acima. Como alternativa, você pode gerar uma licença de Raiz aplicando uma política de DRM ( `setSelectedPolicy()`) e um URL do servidor de licença ( `setLicenseServerURL()`) em vez de metadados.

>[!NOTE]
>
>O URL do License Server é necessário mesmo se não houver um Adobe Primetime DRM License Server do qual os clientes possam solicitar uma licença. Nesse caso, o URL do License Server deve especificar um URL que identifique o emissor da licença.

Se a política de DRM usar o Encadeamento de Licenças Avançado, você deverá especificar uma credencial do License Server para descriptografar a Chave de Criptografia Raiz na política de DRM ( `setRootKeyRetrievalInfo()`).

Se a política de DRM exigir uma licença vinculada ao domínio, use `setDomainCAs()` para especificar os emissores de domínio dos quais o servidor de licença aceita tokens de domínio. Um ou mais certificados de autoridade de certificação de domínio devem ser fornecidos para validar o destinatário da licença.

Se a política de DRM exigir a entrega remota de chaves para dispositivos iOS, você deve fornecer o Certificado de Servidor de Chave aplicando `setKeyServerCertificate()` a menos que um Folheto Interligado esteja sendo gerado.

Para gerar uma licença, você deve invocar `generateLicense()` e especificar o tipo de licença (Folha ou Raiz) e um ou mais certificados de recipient. O certificado do recipient representa um certificado de máquina ou de domínio, dependendo dos requisitos especificados na política de DRM. Se você gerar uma Folha encadeada, um recipient não será necessário. Depois que a licença tiver sido gerada, você poderá substituir as regras de uso que foram especificadas na política de DRM. Por fim, você precisa invocar `signLicense()` para assinar a licença e obter uma instância de `PreGeneratedLicense`. A licença agora pode ser salva (use `getBytes()` para recuperar a licença serializada ou incorporada ao conteúdo criptografado.

Consulte [Incorporando licenças](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

Consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` no diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência para obter um código de amostra sobre como demonstrar licenças pré-geradas.
