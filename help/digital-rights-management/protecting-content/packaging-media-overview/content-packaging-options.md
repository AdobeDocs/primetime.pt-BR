---
title: Opções de empacotamento
description: Opções de empacotamento
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Opções de empacotamento{#packaging-options}

Há várias opções disponíveis para o conteúdo do empacotamento. Você pode especificar as opções na interface `DRMParameters` e implementar as classes que podem interface. Com essas classes, você pode definir parâmetros de assinatura e chave, bem como indicar se deseja criptografar conteúdo de áudio, conteúdo de vídeo ou dados de script. Para ver como eles são implementados na implementação de referência, consulte as descrições das opções de linha de comando do Media Packager discutidas em *Uso das implementações de referência do DRM do Adobe Primetime*. Essas opções são baseadas na API do Java e, portanto, estão disponíveis para uso programático.

As opções de empacotamento incluem:

* Opções de criptografia (áudio, vídeo, criptografia parcial).
* URL do servidor de licenças que o cliente usa como URL base para todas as solicitações que estão sendo enviadas para o servidor de licenças
* Certificado de transporte do servidor de licenças
* Certificado do servidor de licenças, usado para criptografar o CEK
* Credencial do pacote para assinar metadados

