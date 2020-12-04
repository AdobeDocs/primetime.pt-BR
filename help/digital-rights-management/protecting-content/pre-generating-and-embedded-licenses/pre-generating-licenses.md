---
description: Se você usar o Adobe Primetime DRM Professional, poderá pré-gerar licenças e incorporar licenças ao conteúdo. Este recurso pode ser combinado com Encadeamento de Licenças Avançado, de modo que uma licença Leaf é pré-gerada e incorporada no conteúdo, e o cliente pode solicitar uma licença Raiz (vinculada a uma máquina ou domínio) de um servidor de licenças. Como alternativa, os aplicativos clientes podem implementar um fluxo de trabalho no qual o dispositivo faz o pré-registro em um servidor, o servidor gera previamente as licenças que estão vinculadas a esse dispositivo e o cliente recupera suas licenças de um servidor web HTTP simples.
seo-description: Se você usar o Adobe Primetime DRM Professional, poderá pré-gerar licenças e incorporar licenças ao conteúdo. Este recurso pode ser combinado com Encadeamento de Licenças Avançado, de modo que uma licença Leaf é pré-gerada e incorporada no conteúdo, e o cliente pode solicitar uma licença Raiz (vinculada a uma máquina ou domínio) de um servidor de licenças. Como alternativa, os aplicativos clientes podem implementar um fluxo de trabalho no qual o dispositivo faz o pré-registro em um servidor, o servidor gera previamente as licenças que estão vinculadas a esse dispositivo e o cliente recupera suas licenças de um servidor web HTTP simples.
seo-title: Licenças pré-geradoras
title: Licenças pré-geradoras
uuid: aa7d5038-5a9b-40a2-a240-266622158b43
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---


# Pré-gerando licenças {#pre-generating-licenses}

Se você usar o Adobe Primetime DRM Professional, poderá pré-gerar licenças e incorporar licenças ao conteúdo. Este recurso pode ser combinado com Encadeamento de Licenças Avançado, de modo que uma licença Leaf é pré-gerada e incorporada no conteúdo, e o cliente pode solicitar uma licença Raiz (vinculada a uma máquina ou domínio) de um servidor de licenças. Como alternativa, os aplicativos clientes podem implementar um fluxo de trabalho no qual o dispositivo faz o pré-registro em um servidor, o servidor gera previamente as licenças que estão vinculadas a esse dispositivo e o cliente recupera suas licenças de um servidor web HTTP simples.

Se desejar pré-gerar licenças, você deve usar `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obter uma instância de `LicenseFactory`. Você deve especificar uma credencial do License Server para assinar as licenças geradas por essa fábrica. Esta classe suporta a geração de licenças Leaf sem encadeamento de licença e licenças Leaf e Root com [Cadeamento de licença aprimorado](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

Ao gerar uma licença Folha, você deve especificar os metadados de conteúdo que aplicam `initContentInfo()`. Se os metadados incluírem várias políticas de DRM, ou se você quiser usar uma política de DRM que não tenha sido incluída nos metadados, use `setSelectedPolicy()` para especificar a política de DRM para gerar uma licença. Se você usar uma Lista de Atualização de política de DRM para rastrear atualizações de políticas de DRM, poderá fornecer a Lista de Atualização de política de DRM ao License Fatory antes de inicializar os metadados com `setPolicyUpdateList()`.

Ao gerar uma licença raiz, você deve especificar os metadados do conteúdo conforme descrito acima. Como alternativa, você pode gerar uma licença raiz aplicando uma política de DRM ( `setSelectedPolicy()`) e um URL do servidor de licença ( `setLicenseServerURL()`) em vez de metadados.

>[!NOTE]
>
>Um URL do License Server é necessário mesmo se não houver um Adobe Primetime DRM License Server do qual os clientes possam solicitar uma licença. Nesse caso, o URL do License Server deve especificar um URL que identifique o emissor da licença.

Se a política de DRM usar o Encadeamento aprimorado de licença, você deverá especificar uma credencial do License Server para descriptografar a chave de criptografia raiz na política de DRM ( `setRootKeyRetrievalInfo()`).

Se a política de DRM exigir uma licença vinculada ao domínio, você deverá usar `setDomainCAs()` para especificar os emissores de domínio dos quais o servidor de licença aceita tokens de domínio. Um ou mais certificados de CA de domínio devem ser fornecidos para validar o recipient de licença.

Se a política de DRM exigir delivery de chave remota para dispositivos iOS, você deverá fornecer o Certificado de Servidor de Chave aplicando `setKeyServerCertificate()` a menos que um Folheto Interligado esteja sendo gerado.

Se quiser gerar uma licença, chame `generateLicense()` e especifique o tipo de licença (Folha ou Raiz) e um ou mais certificados de recipient. O certificado de recipient representa um certificado de máquina ou de domínio, dependendo dos requisitos especificados na política de DRM. Se você gerar uma Folha com cobertura, um recipient não é necessário. Depois que a licença for gerada, você poderá substituir as regras de uso que foram especificadas na política de DRM. Finalmente, você precisa chamar `signLicense()` para assinar a licença e obter uma instância de `PreGeneratedLicense`. A licença agora pode ser salva (use `getBytes()` para recuperar a licença serializada ou incorporada ao conteúdo criptografado.

Consulte [Incorporando licenças](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

Consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` no diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência para obter exemplos de código sobre como demonstrar licenças pré-geradas.
