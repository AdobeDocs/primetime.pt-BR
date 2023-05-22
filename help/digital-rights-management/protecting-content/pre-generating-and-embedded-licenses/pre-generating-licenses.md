---
description: Se você usa o Adobe Primetime DRM Professional, é possível pré-gerar licenças e incorporar licenças ao conteúdo. Esse recurso pode ser combinado com o Encadeamento de licenças aprimorado, de modo que uma licença do Leaf seja pré-gerada e incorporada ao conteúdo, e o cliente possa solicitar uma licença do Root (vinculada a uma máquina ou domínio) de um servidor de licenças. Como alternativa, os aplicativos clientes podem implementar um fluxo de trabalho em que o dispositivo pré-registra em um servidor, o servidor pré-gera licenças vinculadas a esse dispositivo e o cliente recupera suas licenças de um servidor Web HTTP simples.
title: Licenças pré-geradas
exl-id: 6ced7dde-b4bb-470d-bdae-3042f5577b67
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Licenças pré-geradas {#pre-generating-licenses}

Se você usa o Adobe Primetime DRM Professional, é possível pré-gerar licenças e incorporar licenças ao conteúdo. Esse recurso pode ser combinado com o Encadeamento de licenças aprimorado, de modo que uma licença do Leaf seja pré-gerada e incorporada ao conteúdo, e o cliente possa solicitar uma licença do Root (vinculada a uma máquina ou domínio) de um servidor de licenças. Como alternativa, os aplicativos clientes podem implementar um fluxo de trabalho em que o dispositivo pré-registra em um servidor, o servidor pré-gera licenças vinculadas a esse dispositivo e o cliente recupera suas licenças de um servidor Web HTTP simples.

Se quiser pré-gerar licenças, use `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obter uma instância de `LicenseFactory`. Você deve especificar uma credencial de Servidor de Licenças para assinar as licenças geradas por esta fábrica. Esta classe dá suporte à geração de licenças Leaf sem encadeamento de licenças e de licenças Leaf e Root com o [Encadeamento de licenças aprimorado](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

Ao gerar uma licença Leaf, você deve especificar os metadados de conteúdo que se aplicam `initContentInfo()`. Se os metadados incluírem várias políticas de DRM ou se você quiser usar uma política de DRM que não foi incluída nos metadados, é necessário usar `setSelectedPolicy()` para especificar a política de DRM para gerar uma licença. Se você usar uma Lista de atualização de política DRM para rastrear atualizações de políticas DRM, poderá fornecer a Lista de atualização de política DRM ao License Fatory antes de inicializar os metadados com `setPolicyUpdateList()`.

Ao gerar uma licença Raiz, você deve especificar os metadados de conteúdo conforme descrito acima. Como alternativa, você pode gerar uma licença Raiz aplicando uma política DRM ( `setSelectedPolicy()`) e um URL de servidor de licença ( `setLicenseServerURL()`) em vez de metadados.

>[!NOTE]
>
>Um URL do License Server será necessário mesmo se não houver um Adobe Primetime DRM License Server do qual os clientes possam solicitar uma licença. Nesse caso, o URL do License Server deve especificar um URL que identifique o emissor da licença.

Se a política DRM usar Encadeamento de Licenças Aprimorado, você deverá especificar uma credencial de Servidor de Licenças para descriptografar a Chave de Criptografia Raiz na política DRM ( `setRootKeyRetrievalInfo()`).

Se a política DRM exigir uma licença de domínio vinculado, você deverá usar `setDomainCAs()` para especificar os emissores de Domínio dos quais o servidor de licenças aceita tokens de domínio. Um ou mais certificados da autoridade de certificação de domínio devem ser fornecidos para validar o destinatário da licença.

Se a política DRM exigir a entrega remota de chaves para dispositivos iOS, você deverá fornecer o Certificado de Servidor de Chaves aplicando `setKeyServerCertificate()` a menos que uma folha encadeada esteja sendo gerada.

Se quiser gerar uma licença, você deverá chamar `generateLicense()` e especifique o tipo de licença (Folha ou Raiz) e um ou mais certificados de recipient. O certificado de destinatário representa um certificado de computador ou de domínio, dependendo dos requisitos especificados na política DRM. Se você gerar uma Folha encadeada, um recipient não será necessário. Depois que a licença for gerada, você poderá substituir as regras de uso especificadas na política DRM. Por fim, é necessário invocar `signLicense()` para assinar a licença e obter uma instância de `PreGeneratedLicense`. A licença agora pode ser salva (use `getBytes()` para recuperar a licença serializada ou incorporada ao conteúdo criptografado.

Consulte [Incorporação de licenças](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

Consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` no diretório &quot;samples&quot; de Ferramentas de linha de comando de implementação de referência para código de amostra sobre como demonstrar licenças pré-geradas.
