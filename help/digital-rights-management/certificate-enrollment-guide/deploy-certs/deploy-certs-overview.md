---
title: Visão geral da implantação de certificados
description: Visão geral da implantação de certificados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Visão geral {#deploy-certificates-overview}

Para adicionar certificados aos arquivos de propriedades do Adobe Primetime DRM, converta o arquivo PKCS#7 em um arquivo PFX usando a chave privada e gere um arquivo PEM ou um arquivo DER.

* Quando uma credencial (certificado e chave privada) é necessária, as ferramentas de linha de comando do Primetime DRM e o Adobe HTTP Dynamic Streaming packager exigem um arquivo PFX. O SDK, a implementação de referência e o servidor DRM Primetime para transmissão protegida podem aceitar um arquivo PFX e também podem usar uma credencial armazenada em um HSM.
* Quando apenas um certificado é necessário, a maioria dos componentes de DRM do Primetime pode usar um arquivo PEM, um arquivo DER ou um certificado em um HSM. O Adobe HTTP Dynamic Streaming packager só aceita arquivos DER para certificados.