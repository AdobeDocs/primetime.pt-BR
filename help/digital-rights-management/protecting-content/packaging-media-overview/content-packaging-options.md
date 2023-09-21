---
title: Opções de empacotamento
description: Opções de empacotamento
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Opções de empacotamento{#packaging-options}

Há várias opções disponíveis para você para o conteúdo de empacotamento. Você pode especificar as opções na caixa suspensa `DRMParameters` e implementar as classes que podem fazer interface. Com essas classes, você pode definir parâmetros de assinatura e chave, bem como indicar se deve criptografar o conteúdo de áudio, conteúdo de vídeo ou dados de script. Para ver como elas são implementadas na implementação de referência, consulte as descrições das opções de linha de comando do Media Packager discutidas em *Uso das implementações de referência do Adobe Primetime DRM*. Essas opções são baseadas na API do Java e, portanto, estão disponíveis para uso programático.

As opções de empacotamento incluem:

* Opções de criptografia (áudio, vídeo, criptografia parcial).
* URL do servidor de licenças que o cliente usa como URL base para todas as solicitações enviadas ao servidor de licenças
* Certificado de transporte do servidor de licenças
* Certificado do servidor de licenças, usado para criptografar o CEK
* Credencial do empacotador para assinar metadados
