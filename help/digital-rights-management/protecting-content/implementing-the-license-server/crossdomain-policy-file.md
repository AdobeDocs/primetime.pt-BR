---
title: Arquivo de política DRM entre domínios
description: Arquivo de política DRM entre domínios
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Arquivo de política DRM entre domínios {#crossdomain-drm-policy-file}

Se o servidor de licença estiver hospedado em um domínio diferente do SWF de reprodução de vídeo, um arquivo de política DRM entre domínios ( [!DNL crossdomain.xml]) é necessária para habilitar o SWF para solicitar licenças de um servidor de licenças. Um arquivo de política DRM entre domínios é representado por um arquivo XML que permite ao servidor indicar que seus dados e documentos estão disponíveis para arquivos SWF servidos de outros domínios. Qualquer arquivo de SWF veiculado em um domínio especificado no arquivo de política DRM entre domínios do servidor de licenças tem permissão para acessar dados ou ativos desse servidor de licenças.

A Adobe recomenda que os desenvolvedores sigam as práticas recomendadas ao implantar o arquivo de política entre domínios, permitindo somente que domínios confiáveis acessem o servidor de licença e limitando o acesso ao subdiretório de licença no servidor da Web.

Para obter mais informações sobre arquivos de política DRM entre domínios, consulte os seguintes locais:

* Controles de site (arquivos de política DRM)
* Especificação de arquivo de política DRM entre domínios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

