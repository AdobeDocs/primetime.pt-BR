---
title: Visão geral da implantação de certificados
description: Visão geral da implantação de certificados
copied-description: true
exl-id: 45a4bc7e-f987-4b9a-885d-d989d09566c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Visão geral {#deploy-certificates-overview}

Para adicionar certificados aos arquivos de propriedades do Adobe Primetime DRM, converta o arquivo PKCS#7 em um arquivo PFX usando a chave privada e gere um arquivo PEM ou DER.

* Quando uma credencial (certificado e chave privada) é necessária, as ferramentas de linha de comando do Primetime DRM e o empacotador de HTTP Dynamic Streaming de Adobe exigem um arquivo PFX. O SDK, a implementação de referência e o servidor DRM Primetime para transmissão protegida podem aceitar um arquivo PFX e também podem usar uma credencial armazenada em um HSM.
* Quando apenas um certificado é necessário, a maioria dos componentes DRM do Primetime pode usar um arquivo PEM, arquivo DER ou um certificado em um HSM. O empacotador Adobe HTTP Dynamic Streaming aceita apenas arquivos DER para certificados.
