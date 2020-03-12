---
seo-title: Opções de empacotamento
title: Opções de empacotamento
uuid: 04244428-cb42-438a-8f16-91532c70ea60
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Opções de empacotamento{#packaging-options}

Existem várias opções disponíveis para o conteúdo do empacotamento. Você pode especificar as opções na `DRMParameters` interface e implementar as classes que podem ser interface. Com essas classes, você pode definir parâmetros de assinatura e chave, bem como indicar se deseja criptografar conteúdo de áudio, conteúdo de vídeo ou dados de script. Para ver como eles são implementados na implementação de referência, consulte as descrições das opções de linha de comando do Media Packager discutidas em *Uso das Implementações* de referência do Adobe Primetime DRM. Essas opções são baseadas na API Java e, portanto, estão disponíveis para uso programático.

As opções de empacotamento incluem:

* Opções de criptografia (áudio, vídeo, criptografia parcial).
* URL do servidor de licenças que o cliente usa como URL base para todas as solicitações enviadas para o servidor de licenças
* Certificado de transporte do servidor de licenças
* Certificado do servidor de licença, usado para criptografar o CEK
* Credencial do Packager para assinar metadados

