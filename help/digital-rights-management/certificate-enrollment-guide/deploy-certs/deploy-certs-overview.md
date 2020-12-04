---
seo-title: Visão geral da implantação de certificados
title: Visão geral da implantação de certificados
uuid: e6413f9f-69a5-4881-bb13-47a80cf32a48
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Visão geral {#deploy-certificates-overview}

Para adicionar certificados aos arquivos de propriedades do Adobe Primetime DRM, converta o arquivo PKCS#7 em um arquivo PFX usando a chave privada e gere um arquivo PEM ou um arquivo DER.

* Quando uma credencial (certificado e chave privada) é necessária, as ferramentas de linha de comando do Primetime DRM e o Adobe HTTP Dynamic Streaming packager exigem um arquivo PFX. O SDK, a implementação de referência e o servidor DRM Primetime para transmissão protegida podem aceitar um arquivo PFX e também usar uma credencial armazenada em um HSM.
* Quando apenas um certificado é necessário, a maioria dos componentes do Primetime DRM pode usar um arquivo PEM, um arquivo DER ou um certificado em um HSM. O empacotador Adobe HTTP Dynamic Streaming só aceita arquivos DER para certificados.