---
title: Arquivo de política entre domínios
description: Arquivo de política entre domínios
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Arquivo de política entre domínios {#crossdomain-policy-file}

Se o servidor de licença estiver hospedado em um domínio diferente do SWF de reprodução de vídeo, um arquivo de política entre domínios (cross-domain.xml) será necessário para permitir que o SWF solicite licenças do servidor de licença. Um arquivo de política entre domínios é um arquivo XML que fornece ao servidor uma maneira de indicar que seus dados e documentos estão disponíveis para arquivos SWF servidos de outros domínios. Qualquer arquivo SWF servido de um domínio especificado no arquivo de política entre domínios do servidor de licenças tem permissão para acessar dados ou ativos desse servidor de licenças.

O Adobe recomenda que os desenvolvedores sigam as práticas recomendadas ao implantar o arquivo de política entre domínios, permitindo que apenas domínios confiáveis acessem o servidor de licenças e limitando o acesso ao subdiretório de licenças no servidor da Web.

Para obter mais informações sobre arquivos de política entre domínios, consulte os seguintes locais:

* Controles de site (arquivos de política)
* Especificação do arquivo de política entre domínios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

