---
seo-title: Arquivo de política DRM entre domínios
title: Arquivo de política DRM entre domínios
uuid: cb91a85a-1825-4fd7-a25c-880cdbd5c8b8
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Arquivo de política DRM entre domínios {#crossdomain-drm-policy-file}

Se o servidor de licença estiver hospedado em um domínio diferente do SWF de reprodução de vídeo, um arquivo de política DRM entre domínios ( [!DNL crossdomain.xml]) será necessário para permitir que o SWF solicite licenças de um servidor de licença. Um arquivo de política DRM entre domínios é representado por um arquivo XML que permite ao servidor indicar que seus dados e documentos estão disponíveis para arquivos SWF fornecidos de outros domínios. Qualquer arquivo SWF servido de um domínio especificado no arquivo de política DRM entre domínios do servidor de licenças tem permissão para acessar dados ou ativos desse servidor de licenças.

A Adobe recomenda que os desenvolvedores sigam as práticas recomendadas ao implantar o arquivo de política entre domínios, permitindo apenas que domínios confiáveis acessem o servidor de licenças e limitando o acesso ao subdiretório de licenças no servidor Web.

Para obter mais informações sobre arquivos de política DRM entre domínios, consulte os seguintes locais:

* Controles de site (arquivos de política DRM)
* Especificação do arquivo de política DRM entre domínios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

